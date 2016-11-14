Vulkan Flocking: compute and shading in one pipeline!
======================

**University of Pennsylvania, CIS 565: GPU Programming and Architecture, Project 6**

* Xueyin Wan
* Platform: Windows 10, i7-4870 @ 2.50GHz 16GB, NVIDIA GeForce GT 750M 2GB (Personal Laptop)

## Showcase My Result
![alt text](https://github.com/xueyinw/Project6-Vulkan-Flocking/blob/master/showcase.gif "Final Result")

## Analysis
#### Why do you think Vulkan expects explicit descriptors for things like generating pipelines and commands?
In Vulkan, whenever we want to draw a 3D scene from vertices and vertex attributes, we will use command buffers. Command buffers cannot be allocated directly. Instead, they are provided by a pre-allocated GPU command pool. 
So the descriptor here is to help us update the mapping relationship to each buffers during the whole procedure. Once we have a descriptor set, we can update it directly to put specific values in the bindings, and also copy between different descriptor sets.
With the help of descriptor, we could use command buffer with more flexibility.

#### Describe a situation besides flip-flop buffers in which you may need multiple descriptor sets to fit one descriptor layout.
When we have color map, normal map, depth map, etc. and we want to map these to the same scene, we could put them as different descriptor sets in a single descriptor layouy, and during the process we use different sets to fit different stages' needs.

#### What are some problems to keep in mind when using multiple Vulkan queues?
The notion of queues are how work becomes serialised to be passed to the GPU. When using multiple vulkan queues, we need to include sync primitives for queue to wait before processing the submitted work, and signal when the work in this submission is completed.
Also we need to keep in mind that queue can accept different types of work.

#### What is one advantage of using compute commands that can share data with a rendering pipeline?
Save a lot of time and space by reducing I/O operations since compute commands could share data.

### Credits

* [Vulkan examples and demos](https://github.com/SaschaWillems/Vulkan) by [@SaschaWillems](https://github.com/SaschaWillems)
