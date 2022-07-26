---
layout: post
title: "Implementing Wordpress related posts funciton"
author: Summeli
description: "Creating related posts function for Wordpress"
categories:
    - wordpress
tags:
    - wordpress
    - wordpresstheme
    - php
---

I'm running a corporate blog with only one category for blog-posts. Other categories are used for other stuff, and they are rendered in different way. The blog's theme has its own implementation of related posts, but it produces pretty weak results with our current amount of posts. 

The related posts should be found inside same category, with similar tags. If similar tags are not found, then we just return the lates post (which is usually interesting).

### Writing related post support into Wordpress theme

The related posts function will be called from single-post php file. Just after the post we can call 
the ci_get_related_posts to get related blog-posts. 
```php
    $related = ci_get_related_posts( get_the_ID(), 3 );
```

Then we can write the related post function into our functions.php file. The function combines results from several wordpress queries, so it's far from 'fast implementation'. But it really doesn't matter, since the results are cached with CDN anyway. 

```php
function ci_get_related_posts( $post_id, $related_count, $args = array() ) {
    //get categories
    $categories = get_the_terms( $post_id, 'category' );
    if ( empty( $categories ) ) $categories = array();
    $category_list = wp_list_pluck( $categories, 'slug' );
	
	//get tags
    $post_tags = get_the_terms( $post_id, 'post_tag' );
    if ( empty( $post_tags ) ) $post_tags = array();
    $tag_list = wp_list_pluck( $post_tags, 'slug' );

    $related_args = array(
        'post_type' => 'post',
        'posts_per_page' => $related_count,
        'post_status' => 'publish',
        'post__not_in' => array( $post_id ),
        'order'=>'DESC',
        'orderby'=>'ID',
        'tax_query' => array(
            'relation' => 'AND',
            array(
                'taxonomy' => 'post_tag',
                'field' => 'slug',
                'terms' => $tag_list,
                'compare'  => 'IN'
            ),
            array(
                'taxonomy' => 'category',
                'field' => 'slug',
                'terms' => $category_list
           )	
       )
    );
	
    $wp_query = new WP_Query( $related_args );
	
    //if we didn't get enough, create a new query with results from the first one
    if( $wp_query->post_count < $related_count){
        $my_post_ids = wp_list_pluck( $wp_query->posts, 'ID' );
        $ignore = $my_post_ids;
        array_push($ignore,$post_id);

        //get remaining posts, with category search
        $remaining_arg = array(
            'post_type' => 'post',
            'posts_per_page' => $related_count - count($my_post_ids),
            'post_status' => 'publish',
            'post__not_in' => $ignore,
            'order'=>'DESC',
            'orderby'=>'ID',
            'tax_query' => array(
                 array(
                    'taxonomy' => 'category',
                    'field' => 'slug',
                    'terms' => $category_list
               )
            )
        );

        $wp_remaining_ids_query = new WP_Query( $remaining_arg );
        array_push($my_post_ids, ...wp_list_pluck( $wp_remaining_ids_query->posts, 'ID' ));

        //combine it all into single query with ids
        $new_args = array(
           'post_type' => 'post',
           'post_status' => 'publish',
           'post__in' => $my_post_ids,
           'order'=>'DESC',
           'orderby'=> 'post__in',
        );

	  //return a query with posts with same tags, and then newest from same category
	 return new WP_Query( $new_args );
	} 
	
    return $wp_query;
}
```