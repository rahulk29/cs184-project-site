# Proposal: rptcam

## Overview

Title: `rptcam`

Summary: For our project, we plan to implement a realistic camera model on top of [`rpt`](https://github.com/ekzhang/rpt),
a Rust pathtracing framework, by adding support for different aperture shapes, lens configurations, and autofocus features.
With this model we will render a series of photorealistic images and highlight photographic features
such as depth of field, bokeh, and lens distortions.

Team members:
* Rahul Kumar (284A)
* Rohan Kumar (184)
* Lucy Meng (184)
* Michael Yu (184)

## Problem Description

Cameras are the lens through which we view rendered scenes.
Having an accurate camera model is critical to making an artificial scene appear photorealistic.
However, fully modelling the optical components of a camera and then simulating light propagation
through those components is prohibitively slow.
Simple thin lens models are insufficient to capture details such as optical aberrations.
Our goal is to implement camera models with reasonable accuracy and performance,
integrate them into a pathtracing renderer, and enable users to easily configure different camera parameters.

## Goals and Deliverables

We hope to implement a realistic camera model on top of `rpt`, a Rust pathtracing framework, by adding support
for different aperture shapes, lens configurations, and autofocus features. To demonstrate this, we hope to
produce the following results:
- Images that show photographic features of certain camera apertures/lenses (e.g. depth of field, bokeh, fisheye lenses, etc.)
- A demo of constrast-based autofocus given a specific subject of interest. Perhaps show different renders of the same scene with different focus points.
- While there isn't an easy numerical metric to measure our system, we can use realistic lens configurations and compare the photographic qualities of the resulting images
    with real images taken with a similar camera.

If things go well, we may also want to experiment with additional lens configurations, and perhaps try to model phenomena like chromatic aberration.

The main questions our project answers are related to the APIs and representations needed to integrate custom lenses and apertures into the existing Rust framework.

## Schedule

Week 1:

Aperture shapes
- Determine the format in which to provide custom aperture shapes to the framework.
- Implement the code for converting this format into something that can be used in Rust.
- Modify the raytracing algorithm to sample from within the given aperture, rather from a circular aperture.

Camera lenses
- Determine the format in which to provide custom lens configurations to the framework (may need to make simplifying assumptions such as the lenses being cylindrically symmetrical).
- Implement the code for converting this format into something that can be used in Rust.

Week 2:

Camera lenses
- Implement code that calculates the refraction through the lenses and modify the ray sampling algorithm to only sample rays that pass through the aperture and hit the sensor.

Week 3:

Camera lenses
- Put together a couple of realistic lens models with reference photos, then test that the framework accurately emulates the real camera.

Autofocus
- Implement contrast-based autofocus, and test this with a lens with a small depth-of-field.

Week 4:

Testing/final products
- Clean up code and fix any bugs
- Put together final renders that were listed in the "Goals and Deliverables" section
- (Stretch) Implement wavelength-dependent effects, such as chromatic aberration

## Resources

We plan to build on top of [`rpt`](https://github.com/ekzhang/rpt), a CPU-based path tracing renderer written in Rust.

References:

["A Realistic Camera Model for Computer Graphics"](https://www.cs.utexas.edu/~fussell/courses/cs395t/lens.pdf)

["Camera Models and Optical Systems Used in Computer Graphics: Part I, Object-Based Techniques"](https://people.eecs.berkeley.edu/~barsky/VisRendPapers/survey1.pdf)

[Physically Based Rendering: Camera Models](https://www.pbr-book.org/3ed-2018/Camera_Models)