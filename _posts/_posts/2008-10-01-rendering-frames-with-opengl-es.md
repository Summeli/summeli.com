---
id: 12
title: 'Rendering frames with OpenGL ES'
date: '2008-10-01T13:19:45+03:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=12'
permalink: /12/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'OpenGL ES'
    - 'Symbian Development'
tags:
    - porting
---

The OpenGL ES frameworks expect to have image size to be powers of two. Therefore we create 256×256 frame and then create our image into it as a sub frame.  
Here is an example of opengl es init function.

```
#include "OpenGLES.h"
_LIT( KTESTDATASNES, "c:\\Data\\test_data\\test_565.mbm");
_LIT( KTESTDATA256x239, "c:\\Data\\test_data\\test_256x239.mbm");
static GLuint    texture;
static GLint format;
static GLint type;
static GLuint textures [2];
static EGLDisplay g_EglDisplay;
static EGLSurface g_EglSurface;
#ifdef OPENGL_ES_BENCHMARK
static CFbsBitmap* iBitmap;
#endif

void InitializeOpenGLES(EGLDisplay aDisplay, EGLSurface aSurface)
{
    #ifdef OPENGL_ES_BENCHMARK
    iBitmap = new (ELeave) CFbsBitmap();
    TInt error = iBitmap->Load( KTESTDATA256x239, 0 );
    TDisplayMode mode = iBitmap->DisplayMode();
    if( mode == EColor64K )
    {
        // 64k maps to RGB565, which we will use as opengl es texture,
        RDebug::Print(_L("Colour mode is correct"));
    }
    RDebug::Print(_L("ConstructL complete"));
    #endif
    g_EglDisplay = aDisplay;
    g_EglSurface = aSurface;
    glClear(GL_COLOR_BUFFER_BIT);
    glClearColor(0.0, 0.0, 0.0, 0.0); // set background to black
    // Textures are initialized in OpenGL ES API by this function.
    glGenTextures( 1, textures[0] );
    //Bind the background texture to iTexturesID[0], set the texture environment.
    glBindTexture( GL_TEXTURE_2D, textures[0] );
    glTexImage2D (GL_TEXTURE_2D, 0, GL_RGB,
    256, 256, 0,
    GL_RGB, GL_UNSIGNED_SHORT_5_6_5, NULL);
    glTexEnvi(GL_TEXTURE_ENV, GL_TEXTURE_ENV_MODE, GL_REPLACE);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glMatrixMode(GL_PROJECTION);
    // Push on a new matrix so that we can just pop it off to go back to perspective mode
    glDisable( GL_DEPTH_TEST );
    glDisable( GL_CULL_FACE  );
    // Reset the current matrix to our identify matrix
    glLoadIdentity();
    // Pass in our 2D ortho screen coordinates (left, right, bottom, top, near, far).
    glOrthof( 0, 1, 0, 1, -1, 1 );
    // Switch to model view so that we can render the texture
    glMatrixMode(GL_MODELVIEW);
    // Initialize the current model view matrix with the identity matrix
    glLoadIdentity();
    glMatrixMode( GL_PROJECTION );
    //glEnable( GL_DEPTH_TEST );
    //glEnable( GL_CULL_FACE  );
}
```

And then the DeInit function. Only texture is deleted in here. The Screen surface is handled elsewhere.

```
void DeInitOpenGLES()
{
    glDeleteTextures(1, textures[0]);
}
```

And here is the putframe function. Currently there are

```
static const GLbyte bgverts[8] =
{
    0, 0,
    1, 0,
    0, 1,
    1, 1
};
static const GLubyte bgtex[8] =
{
    0, 1,
    1, 1,
    0, 0,
    1, 0
};
//Use rotated matrix for N95, since the phone should be turned upside down.
static const GLubyte rot180_bgtex[8] =
{
    1, 0,
    0, 0,
    1, 1,
    0, 1
};
static const GLbyte vertices[3 * 3] =
{
    -1,    1,    0,
    1,   -1,    0,
    1,    1,    0
};
static const GLubyte colors[3 * 4] =
{
    255,      0,    0,    255,
    0,    255,    0,    255,
    0,      0,  255,    255
};
void PutS9xFrame( int aWith, int aHeight )
{
    #ifdef OPENGL_ES_BENCHMARK
    iBitmap->LockHeap();
    TUint8 *data = (TUint8 *) iBitmap->DataAddress();
    glTexSubImage2D (GL_TEXTURE_2D, 0, 0, 8, 256, 239,
    GL_RGB, GL_UNSIGNED_SHORT_5_6_5, data);
    iBitmap->UnlockHeap();
    #else
    //y-offset8, TODO: calculate this for each resolution
    glTexSubImage2D (GL_TEXTURE_2D, 0, 0, 8, 256, 239,
    GL_RGB, GL_UNSIGNED_SHORT_5_6_5, GFX.Screen);
    #endif
    // Enable vertex arrays.
    glEnableClientState( GL_VERTEX_ARRAY );
    // Set array pointers.
    glVertexPointer( 2, GL_BYTE, 0, bgverts );
    // Enable texture arrays
    glEnableClientState( GL_TEXTURE_COORD_ARRAY );
    // Set texture coords
    glTexCoordPointer( 2, GL_BYTE, 0, rot180_bgtex );
    glEnable(GL_TEXTURE_2D);
    glBindTexture( GL_TEXTURE_2D, textures[0] );
    glDrawArrays(GL_TRIANGLE_STRIP, 0, 4);
    glDisable(GL_TEXTURE_2D);
    glDisableClientState(GL_TEXTURE_COORD_ARRAY);
    glDisableClientState(GL_VERTEX_ARRAY);
    // Go back to model view matrix
    glMatrixMode( GL_MODELVIEW );
    eglSwapBuffers( g_EglDisplay, g_EglSurface);
}
```

Benchmarking the OpenGL ES renderer. I decided to run the rendering of bitmap in a loop and then calculate the average FPS from 1000 frames. This should be quite accurate way of doing it.
´´´
TTime starttime;  
starttime.HomeTime();  
for( TInt i=0; i
´´´