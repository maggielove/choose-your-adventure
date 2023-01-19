# Type/Code frontend dev exercise
​
## Instructions
​
For this exercise, you are tasked with implementing a choose-your-own-adventure style app, following the UI designs (which can be found under `designs/`) and the functional requirements as detailed further below.
​
We ask that you complete this project in vuejs (v2 not v3) - if vue is new to you that will be taken into consideration during review.
​
Work on your implementation directly in this directory, and submit it to us by zipping it up and sending it to [seth@typecode.com](mailto:seth@typecode.com), or by sharing a _private_ repository on Github with [ssyberg](https://github.com/ssyberg). As part of your solution, replace this README with instructions for spinning up the project (including installing any dependencies, etc) and any other relevant project details you might include in a project readme (does not have to be extensive). Please omit any third-party installable dependencies (such as `node_modules/`).
​
You're not required to do the exercise in one sitting-- you can work on it over the course of multiple sittings if you want. We expect it to take approximately 6-12 hours, and will likely be curious, after reviewing your solution, how long it took you and which parts were most time consuming (please keep track of your time).
​
### Structural requirements
​
Approach this project as a first sprint in a project that will grow much larger/complex. As such you should make structural/organizational decisions that will scale well to a large development project (though *performance* scaling need not be considered).
​
### Functional requirements
​
Note an `assets` directory has been provided for fonts, images, and data.
​
This exercise should run as a single page app in a browser. The only browser you're required to support is the latest version of Google Chrome. The included UI designs show examples of what the UI should look like at desktop viewport sizes, but we are looking for you to reinterpret the layout as you see fit, so that it stays sensible on smaller viewport sizes.
​
The app consists of a set of frames that the user navigates through via buttons. Only one frame is visible to the user at a time, and the frame always fills the entire viewport. If the contents of a frame are taller than the height of viewport, the frame's height should increase past the fold to fit all of its content, and the user should be able to scroll the page to see the entire frame. If the frame's contents are shorter than the viewport height, the frame should be exactly as tall as the viewport.
​
Each frame (except for the "Loading" frame discussed below) follows a common template. The actual frames and their contents are populated based on a story JSON file (`/assets/story.json`), which the app should load using AJAX upon initialization.
​
This JSON file includes a **frames** array of frame objects. Each frame object consists of the following fields (note that some of these fields are optional), that affect how the frame is rendered and how it behaves.
- Header text displayed in each frame.
- Body HTML content displayed in each frame.
- An optional image, represented as a relative path to its source file, to be dislayed with the body content. Note that the body content doesn't wrap around the image if it's taller than the image - it just continues to grow in its column.
- A map of color hex values, containing:
    - The background color of the entire frame.
    - The foreground color used in the frame for text, borders, etc.
- A list of button objects. A frame can have zero, one, or two buttons. If the frame has one button, the button is displayed in the frame's lower right corner. If the frame has two buttons, the first button is displayed in the lower left corner, the second in the lower right.
    - The label to display for the button.
    - The index of a target frame to show when the user clicks the button. The frame's index is with respect to its index position in the **frames** array.
​
Each frame displays a frame number in its upper right corner. The frame number is derived from the frame's index position in the **frames** array. The 0 index frame's number is 1, the 1 index frame is 2, and so on.
​
While the request to load the story data is pending, a "Loading" frame is displayed. The text/colors of this frame are baked into the app. Once the story data has loaded, the first frame in the **frames** array should automatically be shown.
