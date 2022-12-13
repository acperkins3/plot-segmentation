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
 
<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fecb219f6-3001-4cd5-a337-8f7606e497f8%2FScreen_Shot_2021-08-30_at_11.46.33_PM.png?id=3b645b91-3960-46eb-819a-0e9507ae8661&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" width="300" /></p>

3. Zoom in on the ground control point such that you can see it well and then click on the yellow star button (circled below)
<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3fc41c4e-03e0-4f19-9d3e-d9f6ab9a02df%2FScreen_Shot_2021-08-30_at_11.48.41_PM_copy.png?id=11466b4f-4c7a-4638-8d59-366c63ed1163&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" /></p>

4. Click on the center of the bucket lid and a window will come up asking for the coordinates. You can copy and paste from below (the first number is the `X/East` and the second number is `Y/North`

<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F970ca09f-f89a-4bc7-a5a4-169309e2e517%2FScreen_Shot_2022-12-13_at_9.12.31_AM.png?id=d14a42ca-4c11-477b-9bc3-577d21f1e98c&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" /></p>

### K17

Top Left of the image

```
-89.55515305359941181
```

```
44.119294653000523
```

Top Right

```
-89.55276674158479011
```

```
44.1192641828970622
```

Bottom Right

```
-89.55277375393758632
```

```
44.11886313902382284
```

Bottom Left

```
-89.55518660140415932
```

```
44.1189022223115046
```

5. In the settings (the gear) make sure the `Transformation type` is set for `Polynomial 1` and that `Save GCP points` is checked. By default, the output is named the same as the input with `_modified` at the end of the file name, which is good to know. It doesn't modify or change the file we started with.

<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F06800fc4-7fc4-4bac-98b0-99fbc53d101a%2FScreen_Shot_2022-12-13_at_10.19.44_AM.png?id=8de221f1-48ef-4bce-9da7-fce36bf2e14e&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" /></p>

6. After clicking OK on the Transformation Settings, click the green play button in the menu bar to start running the georeferencing.

<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F12f36085-5d33-4dfe-86ba-0d7a28c5c7d3%2FScreen_Shot_2022-12-13_at_10.22.54_AM.png?id=78469212-7b18-46ed-9f1e-b3a961c74deb&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" width="300" /></p>

## Adjusting Plot Boundaries

1. Drag an orthomosaic file into QGIS to open it. If the orthomosaic has been georeferenced, the name is probably `Ortho1_QGIS_modified.tif`.
2. Drag the plot boundaries file into QGIS to open it. This should be called `K17_Plots.gpkg` (for K17, for example).
3. To choose how the plots are displayed, right click on the plots object in the sidebar and choose `Properties...` Under `Symbology`, you can reduce the opacity to make the rectangles more transparent. You can also click on one of the outlines below

<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3ab21842-2c9b-4163-8af4-628d275a6022%2FScreen_Shot_2022-12-13_at_10.54.47_AM.png?id=2af53feb-32cc-434e-ad6f-74271e87a382&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" /></p>

4. This is probably not necessary, but if you want to plot numbers to be displayed, click the `Labels` tabl, choose `Single Labels` from the dropdown at the top, and set `Value` to `PlotID` in the dropdown.

<p align="center"><img src="https://speckled-breadfruit-5bb.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F93211299-1908-4298-957d-570ce6941cb5%2FScreen_Shot_2022-12-13_at_10.58.43_AM.png?id=83656726-d330-40bd-9882-5d92a836092c&table=block&spaceId=5c4f5b44-950a-4844-bd0f-87f77e11832b&width=2000&userId=&cache=v2" /></p>

