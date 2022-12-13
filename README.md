# plot-segmentation
Information for our plot segmentation

## Big Picture

Our goal is to put rectangle bounding boxes around the plots so that we can crop the images to that area and have mostly just plants from that plot in the cropped image. Since the GPS coordinates are not very stable between flights, doing the georeferencing step first may help. If that's not possible (because the ground control points can't be seen, for example) or not helpful, that can be skipped. 

There will be a separate `Plots.gpkg` file for every flight at the end, and they can live in the folder that is named with the data of that flight.

## Georeferencing

This is the process where we tell the software what the GPS coordinates of certain points are so that it can update the GPS coordinate system for the image.

The points we use are the red bucket lids in the corners of the fields, which we call ground control points. There need to be at least 3 ground control points visible in the picture for georeferencing to work, so if there are fewer than that, this step should be skipped.

1. To start, click `Raster` > `Georeferencer` from the menu toolbar on a Mac, or ___ on a PC.
2. Click the blue checkered button in the top left and open that file that will be georeferenced
<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fecb219f6-3001-4cd5-a337-8f7606e497f8%2FScreen_Shot_2021-08-30_at_11.46.33_PM.png?id=3b645b91-3960-46eb-819a-0e9507ae8661&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2"
max-width: 50% /></p>