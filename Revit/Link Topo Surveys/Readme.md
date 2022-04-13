# Revit Link Topo Survey Guide:

Straight to the point guide on how to correctly link (UK - British) Topo Surveys into Revit 2019+ with Project Units set to millimeters. Read the entire guide before implementing in your Revit project, no guarantee is made that the steps are in perfect chronological order!

### Guide Requirements:

The following guide requires and is based on linking a Topo Survey which conforms to the following:

- Purged AutoCAD .DWG
- Drawing setup in Meters[^1] (_Don't change this, Revit will handle the conversion_)
- Drawing setup to 3 decimal precision ideally, 2 decimals can work but may cause issue for rotation.
- Drawing UCS set to WCS [^2]
- Drawing True North is points 0° vertical (x) (_up the page_)
- Drawing contains easting and northing grid lines and references [^3]
- Confirm coordinates using `ID` Command[^4]
- Property boundary (_highly recommended_)
- Remove unnecessary text and lines (_highly recommended_)

## Step 1: Introduction

You NEED to first understand Revit's rather esoteric Origins and Coordinates system, don't base your understanding off of AutoCAD or any other CAD software as things in Revit are subtly different!

1. What is the differences between the Project Base Point & the Survey Point?
   ![Origins_and_Coordinates](Images/Revit_Origin_and_Coords.png?raw=true "Origins and Coordinates")

2. Understand that unlike AutoCAD, Revit has it's own Internal Origin (Startup Location / Revit Origin) and thus a somewhat _abstracted_ internal coordinate system which is separated and does not relate to World Coordinates/Geo Coordinates. If you loose the location of the Internal Origin you can find it by the following:
   ![Revit_Origin](Images/Revit_Origin.png?raw=true "Revit Origin")

3. It's recommended to set and `Pin` reference planes to the Internal Origin along with setting the Project Base Point to the Internal Origin. This will help insure your model is never far from it:
   ![Revit_Origin_Tracking](Images/Revit_Origin_Tracking.png?raw=true "Revit Origin Tracking")

4. Don't model to far from Revit's Internal Origin. Many professionals don't even know there is an Internal Origin and stray far from it, which causes performance and precision issues! Revit has a comfort tolerance of approximately 20miles radius from the Internal Origin, after this Graphical estimation is noticeable! **You will often find that when linking large DWG files, especially Topo Surveys located 10's or even 100's of miles from the DWG origin (0,0,0), Revit will refuse to link these by `Auto - Shared Origin` or `Origin to Origin`.**
   ![Revit_Extents_Issue](Images/Revit_Extents_Issue.png?raw=true "Revit Extents Issue")

## Step 2: Preparations for Linking

Make sure you've followed the above Guide Requirements to correctly setup the Topo Survey .DWG.

1. Ensure your Revit project units are as follows (3 decimal precision is recommended for rotation, but 2 can work):
   ![Revit_Project_Units](Images/Revit_Project_Units.png?raw=true "Revit Project Units")

2. Set the site plan view to True North, as we are importing the Topo aligned to true north.

3. Ensure your Revit Project Base Point and Survey Point are both set to the Internal Origin. If this is a new file and they've not been moved, they should all be located correctly. If you've moved them, right click and move the Project Base Point to Internal Origin, followed by manually moving the Survey Point. **From here we will avoid moving the Project Base Point from the Internal Origin!**
   ![New_Revit_Project](Images/New_Revit_Project.png?raw=true "New Revit Project")

4. Correct settings for linking the Topo Survey. Avoid using Auto-Detect for the `Import Units` setting, match this to what you set within the Topo Survey .DWG's Drawing Setup. Un-tick both: `Correct Lines that are slightly off axis` and `Orient to View` boxes. Set `Positioning` to Origin to Origin or Center to Center, _this may not work if the Topo Survey is over 33km from the AutoCAD origin_. Thus, my recommendation would be to set this to Manual - Center.
   ![Linking_Settings](Images/Linking.png?raw=true "Linking Settings")

## Step 3: Linking and Aligning

Ensure the view you are set to within Revit has it's `Orientation` set to True North!

1. There are a number of approaches to achieve this however, the method I would recommend is to ensure a corner of your building and/or building grid intersection (E.g. A1) are set to the Internal Origin and Project Base Point. If the geo-coordinates for this are known, add a point or insertion point block at this location within the Topo Survey .DWG file. This will provide a usefully reference point once the the Topo Survey is linked:
   ![Topo_Insertion_Point](Images/Topo_Insertion_Point.png?raw=true "Topo Insertion Point")

2. Go ahead and link the Topo Survey .DWG in Revit, following the settings outlined above.

3. Place the linked survey drawing close to the Project Base Point (origin) of the project, this can be achieved easily by using setting `Positioning` to Manual - Center and placing the survey drawing centrally to the Project Base Point.

4. _(Optional) If you followed step 1. Move (MV) the survey drawing by selecting the point or insertion point block reference point and moving it precisely to the Project Base Point:_
   ![Insertion_Point_to_Project_Base_Point](Images/Insertion_Point_to_Project_Base_Point.png?raw=true "Match Insertion reference to PBP")

5. \*(Optional) If the project north rotation from True North is known, this can easily be added by using the Rotate True North tool. Simply enter the rotation factor, ensuring the view you are set to has it's `Orientation` set to True North! Once set the view should remain as is, however, set `Orientation` to Project North will rotate the view by the factor previously entered. (Other tutorials show this step in the revers order, but as of Revit 2019 this method achieves the same outcome!)
   ![Rotate_True_North](Images/Rotate_True_North.png?raw=true "Rotate True North")

6. Now use the `Acquire Coordinates` (AC) tool which was created to let us PULL this information in from the linked Topo Survey .DWG. This method usually works and should avoid the manual process of converting the Topo Survey's eastings and northings from meters to millimeters. _However, if you need to make this change due to the `Acquire Coordinates` not working use the method outlined in this video_: [Aligning Revit models to DWG Surveys]: https://youtu.be/1_F6YRgY6aI?t=1169
   ![Acquire_Coordinates](Images/Acquire_Coordinates.png?raw=true "Acquire Coordinates").

7. At this point the Survey Point will move to the acquired coordinates origin (0,0,0). Zoom way out to find it!
   ![Survey_Point_3](Images/SurveyPoint03.jpg?raw=true "Find Survey Point").

8. It can either be left there or moved to a know point, ideally a **Survey Station Point** or **Grid Intersection Point**. However, before moving the Survey Point, click on the Survey Point and `un-clip` it by clicking on the small clip icon to the side of the Survey Point. This allows you to move the Survey Point without moving the previously Acquire Coordinates (geo-coordinate origin). Precisely move the Survey Point to a desired location and inspect the eastings and northings match what is shown in the Topo Survey .DWG or Survey Station's location as specified within the Survey's Control Schedule (usually provided with Topo Survey).
   ![Survey_Point_4](Images/SurveyPoint04.jpg?raw=true "Move Survey Point").

9. Lastly, re-clip and pin both the Survey Point, Project Base Point and linked Topo Survey drawing so as to not accidentally move these.

## Step 4: Checking

1. Place annotation `Spot Coordinates` at known locations (Grid Intersections, Survey Stations, etc) and confirm the eastings and northings match Topo Survey using the `ID` command within AutoCAD.

2. The annotation `Spot Coordinates` can also be duplicated and within its properties and then alter the `Coordinate Base` to either; Internal Origin, Survey Point, Project Base Point to change the northing and easting (x, y) values relative to Revit's Internal Origin, Survey Point (Survey Origin 0,0,0) or Project Base Point (corner of building) respectively.

## TO-DO

1. Add guide to altering the elevation of the Base Point.
2. Add new guide to cover Shared Coordinates in Revit, which are completely separate to the above!!

## Resources:

### Convert northings and eastings from Meters to Millimeters:

**Survey Point (Station CH10) (Meters):**

```
  N/S (y): 168110.6000
  E/W (x): 574717.5700
  Elevation: 4.847
```

**Survey Point (Station CH10) (Milimeters):**

```
  N/S (y): 168110600.0
  E/W (x): 574717570.0
  Elevation: 4847.0
```
### Useful additional guides

- [Steve Stafford Survey Point Blog 3](https://revitoped.blogspot.com/2015/04/survey-point.html)
- [Steve Stafford Survey Point Blog 4](https://revitoped.blogspot.com/2015/04/survey-point-post-4-acquiring.html)
- [Aligning Revit models to DWG Surveys](https://www.youtube.com/watch?v=1_F6YRgY6aI&t)

## Footnotes:

[^1]: ![Drawing_Setup](Images/Drawing_Setup.png?raw=true "Drawing Setup")
[^2]: ![UCS](Images/UCS.png?raw=true "UCS")
[^3]: ![Survey_Features](Images/Survey_Features.png?raw=true "Survey Features")
[^4]: ![ID_Command](Images/ID_Command.png?raw=true "ID Command")
