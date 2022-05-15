---
id: 2081
title: 'Fast Blit with OpenGL ES 2.0 and texture uploading'
date: '2011-05-10T22:02:11+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2081'
permalink: /2081/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'OpenGL ES'
    - 'Qt Development'
tags:
    - 'OpenGL ES'
    - Qt4
    - scaling
---

OpenGL ES 2.0 is fully shader based, which means you can’t draw any geometry without having the appropriate shaders loaded and bound. This means there is more setup code required to render than there was in OpenGL ES 1.1 with fixed pipeline.  
Setting up the OpenGL ES 2.0 pipeline.

```
void glBlitter::initializeGL ()
{
    GLuint fragmentShader;
    GLuint vertexShader;
    GLint linked;
    glDepthFunc(GL_ALWAYS);
    glDisable(GL_DEPTH_TEST);
    glDisable(GL_STENCIL_TEST);
    glDisable(GL_CULL_FACE);
    //Vertex shader
    QString srcVertShader =
        "attribute vec4 a_position; \n"
        "attribute vec2 a_texCoord; \n"
        "varying vec2 v_texCoord; \n"
        "void main() \n"
        "{ \n"
        " gl_Position = a_position; \n"
        " v_texCoord = a_texCoord; \n"
        "} \n";
    //fragment shader
    QString srcFragShader =
        "precision mediump float; \n"
        "varying vec2 v_texCoord; \n"
        "uniform sampler2D s_texture; \n"
        "void main() \n"
        "{ \n"
        " gl_FragColor = texture2D( s_texture, v_texCoord );\n"
        "} \n";
    // Create the program object
    m_program = glCreateProgram();
    if(!m_program)
      return;
    // Load the shaders
    vertexShader = loadShader(qPrintable(srcVertShader), GL_VERTEX_SHADER);
    fragmentShader = loadShader(qPrintable(srcFragShader), GL_FRAGMENT_SHADER);
    glAttachShader(m_program, vertexShader);
    glAttachShader(m_program, fragmentShader);
    // Link the program
    glLinkProgram(m_program);
    // Check the link status
    glGetProgramiv(m_program, GL_LINK_STATUS, &linked);
    if(!linked){
      GLint infoLen = 0;
      glGetProgramiv(m_program, GL_INFO_LOG_LENGTH, &infoLen);
      if(infoLen > 1){
        char* infoLog = (char*)malloc(sizeof(char) * infoLen);
        glGetProgramInfoLog(m_program, infoLen, NULL, infoLog);
        qDebug() << infoLog;
        free(infoLog);
      }
      glDeleteProgram(m_program);
      return;
    }
    m_posLoc = glGetAttribLocation ( m_program, "a_position" );
    m_texLoc = glGetAttribLocation ( m_program, "a_texCoord" );
    // Get the sampler location
    m_samplerLoc = glGetUniformLocation ( m_program, "s_texture" );
    //Init textures to plot in the paintgl function
    InitTextures();
    glClearColor(.3,.4,.6,1);
}
```

The actual drawing is done in the QGLWidget’s paintGL function. The OpenGL ES 2.0 guild line says that you should use upload textures with sizes of power of two. However you don’t have blit the whole texture. You can create a texCoords matrix for using only a part of the uploaded texture. There’s a really good tutorial for texturemapping in [iPhone Development Blog](http://iphonedevelopment.blogspot.com/2009/05/opengl-es-from-ground-up-part-6_25.html). It’s for iPhone and it’s for OpenGL ES 1.1 or so, but the vector math in binding the textures etc. is still valid with OpenGL ES 2.0.  
  
Here’s my example of painGL and texture blitting.

```
void glBlitter::paintGL()
{
   glClear( GL_COLOR_BUFFER_BIT );
   // Use the program object
   glUseProgram ( m_program );
   glVertexAttribPointer( m_posLoc, 2, GL_FLOAT, GL_FALSE, 2 * sizeof(GLfloat), vertexCoords );
   glVertexAttribPointer( m_texLoc, 2, GL_FLOAT, GL_FALSE, 2*sizeof(GLfloat), texCoords );
   glEnableVertexAttribArray( m_posLoc );
   glEnableVertexAttribArray( m_texLoc );
   glBindTexture(GL_TEXTURE_2D, m_textures[0] );
   //copy the emulator's virtual framebuffer into a texture
   copyScreen( m_ScreenPtr, BaseAddress );
   //upload the texture
   glTexSubImage2D( GL_TEXTURE_2D,0,
             0,0, 256,256,
             GL_RGB,GL_UNSIGNED_SHORT_5_6_5, m_ScreenPtr );
   //sampler texture unit to 0
   glUniform1i( m_samplerLoc, 0 );
   glDrawElements( GL_TRIANGLES, 6, GL_UNSIGNED_SHORT, indices );
}
```

You can also download the whole glBlitter.cpp from here: [glBlitter.cpp](/wp-content/uploads/2011/05/glBlitter.cpp)