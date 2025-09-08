# Raytracer

A multithreaded raytracer implementation in C++ that renders 3D scenes using ray tracing algorithms. This project demonstrates computer graphics concepts including physically based materials, camera models, and multithreading. 

The raytracer works by sending rays from the camera through pixels and calculating the colors of intersection points. The rays may go through multiple objects, and in that case only the nearest object is taken into consideration.

The color of the pixel is based on the material of the object the ray hits. For metal the ray is reflected, for lambertian the ray is randomly scattered, and for dielectric the ray passes through. The ray keeps bouncing around the scene until it either hits the sky or bounces too many times. Each bounce multiplies the color, where each material that the ray bounces off of filters the light coming towards it. For dielectric objects the refraction of light is simulated using Snell's Law and the reflection of light is determined by Schlick's approximation.

Anti-aliasing was implemented by taking multiple samples per pixel by treating it like it's a small square. Rays are sent towards random offsets from the center of the pixel and the color for that ray is determined. The color for the pixel is the average of all of the samples taken resulting in less jagged edges.

The thin lens approximation to simulate depth of field. Instead of all rays originating from a single point, the camera aperture is modeled as a disk from which rays are randomly sampled. Objects at the focal distance remain sharp, while objects closer or farther appear blurred. The amount of blur depends on the aperture size (defocus angle) and the distance from the focal plane.

Multithreading was added to significantly speed up rendering time by distributing the workload across multiple threads. This works since the calculation for each pixel color is completely independant. The image is divided into chunks based on the number of available threads, with each thread responsible for rendering a specific range of rows. An image buffer stores the calculated pixel colors. This parallel approach reduces rendering time substantially compared to single-threaded execution.