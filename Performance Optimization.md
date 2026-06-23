Performance Optimization Challenge (Java)
Selected Scenario
Optimize Memory Usage (Java – ImageProcessor)

Problem Description
The application crashes with the following error:

java.lang.OutOfMemoryError: Java heap space

This error occurs when the program attempts to use more memory than is available to the Java Virtual Machine (JVM).

Root Cause
The application loads all images into memory at the same time.

List<BufferedImage> images = new ArrayList<>();
List<BufferedImage> processedImages = new ArrayList<>();
When a large number of high-resolution images are processed, memory usage increases significantly and eventually exceeds the available heap space.

Suggested Solution
Process images one at a time instead of storing all images in memory.

Example approach:

for (File imageFile : imageFiles) {
    BufferedImage image = ImageIO.read(imageFile);

    BufferedImage processed = applyEffects(image);

    String outputName = outputFolder + File.separator +
            "processed_" + imageFile.getName();

    ImageIO.write(processed,
            getImageFormat(imageFile.getName()),
            new File(outputName));
}
This approach reduces memory usage because each image can be released after processing.

Performance Results
Before Optimization
All images stored in memory simultaneously

High memory consumption

Application may fail when processing 50–100 images

OutOfMemoryError occurs

After Optimization
Images processed individually

Lower memory consumption

More efficient resource usage

No OutOfMemoryError

Learning Points
Avoid loading large amounts of data into memory unnecessarily.

Process files in smaller batches where possible.

Release objects that are no longer required.

Monitor memory usage when working with large files or images.

Reflection
This exercise demonstrated that performance problems are not always caused by slow code.
Memory management is equally important. 
Processing one item at a time is often more efficient than loading all data into memory before processing it.

  
