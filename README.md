# glsl-bezier-curve
Bezier curve ported to an NPM package for [glslify](http://github.com/chrisdickinson/glslify).

## Installation
`npm install glsl-bezier-curve`

## Usage ##
``` glsl

attribute vec3 position;

uniform mat4 uModelMatrix;
uniform mat4 uViewMatrix;
uniform mat4 uProjectionMatrix;
uniform float uTime;

#pragma glslify: bezier = require(glsl-bezier-curve)

void main() {
  vec3 start    = vec3(2.0, 0.0, 0.0);
  vec3 end      = vec3(-2.0, 0.0, 0.0);
  vec3 control1 = vec3(1.0, 2.0, 0.0);
  vec3 control2 = vec3(-1.0, -2.0, 0.0);
  float time    = fract(uTime * 0.5);

  vec3 posOffset = bezier(start, control1, control2, end, time);
  
  gl_Position = uProjectionMatrix * uViewMatrix * uModelMatrix * vec4(position + posOffset, 1.0);
}
```