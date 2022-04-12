# Revit Link Topo Survey Guide:

Straight to the point guide on how to correctly link (UK - British) Topo Surveys into Revit 2019+ with Project Units set to millimeters.

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
   ![Origins_and_Coordinates](Revit/Link%20Topo%20Surveys/Images/Revit_Origin_and_Coords.png "Origins and Coordinates")

2. Understand that unlike AutoCAD, Revit has it's own Internal Origin (Startup Location / Revit Origin) and thus a somewhat _abstracted_ internal coordinate system which is separated and does not relate to World Coordinates/Geo Coordinates. If you loose the location of the Internal Origin you can find it by the following:
   ![Revit_Origin](/Images/Revit_Origin.png "Revit Origin")

3. It's recommended to set and `Pin` reference planes to the Internal Origin along with setting the Project Base Point to the Internal Origin. This will help insure your model is never far from it:
   ![Revit_Origin_Tracking](/Images/Revit_Origin_Tracking.png "Revit Origin Tracking")

4. Don't model to far from Revit's Internal Origin. Many professionals don't even know there is an Internal Origin and stray far from it, which causes performance and precision issues! Revit has a comfort tolerance of approximately 20miles radius from the Internal Origin, after this Graphical estimation is noticeable! **You will often find that when linking large DWG files, especially Topo Surveys located 10's or even 100's of miles from the DWG origin (0,0,0), Revit will refuse to link these by `Auto - Shared Origin` or `Origin to Origin`.**
   ![Revit_Extents_Issue](/Images/Revit_Extents_Issue.png "Revit Extents Issue")

## Step 2: Linking

Make sure you've followed the above Guide Requirements to correctly setup the Topo Survey .DWG!

1. Ensure your Revit project units are as follows (3 decimal precision is recommended for rotation, but 2 can work):
   ![Revit_Project_Units](/Images/Revit_Project_Units.png "Revit Project Units")

2. Set the site plan view to True North, as we are importing the Topo aligned to true north.

3. Ensure your Revit Project Base Point and Survey Point are both set to the Internal Origin. If this is a new file and they've not been moved, they should all be located correctly. If you've moved them, right click and move the Project Base Point to Internal Origin, followed by manually moving the Survey Point. **From here we will avoid moving the Project Base Point from the Internal Origin!**
   ![New Revit Project](/Images/New_Revit_Project.png "New Revit Project")

4. Linking the file within Revit and correct settings. Avoid using Auto-Detect for the `Import Units` setting, match this to what you set within the Topo Survey .DWG's Drawing Setup. Un-tick both: `Correct Lines that are slightly off axis` and `Orient to View` boxes. Set `Positioning` to Origin to Origin, _this may not work if the Topo Survey is over 33km from the AutoCAD origin_. Thus, my recommendation would be to set this to Manual - Center.
   ![Linking_Settings](/Images/Linking.png "Linking Settings")

## Step 3: Align the survey

There are a number of approaches to achieve this however, the method I would recommend is to ensure a corner of your building and/or building grid intersection (E.g. A1) are set to the Internal Origin and Project Base Point. If the geo-coordinates for this are know, I would suggest adding a point or insertion point block at this location within the Topo Survey .DWG file.

## Footnotes:

[^1]: ![Drawing_Setup](/Images/Drawing_Setup.png "Drawing Setup")
[^2]: ![UCS](/Images/UCS.png "UCS")
[^3]: ![Survey_Features](/Images/Survey_Features.png "Survey Features")
[^4]: ![ID_Command](/Images/ID_Command.png "ID Command")
