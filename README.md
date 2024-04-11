# freecad-qtplasmac-postprocessor
Modified linuxcnc postprocessor to output gcode for the qtplasmac controller 

Use at your own risk - works for me/my machine/process!

I use Freecad to model parts that are to be cut on my diy cnc plasma cutter. The 
machine uses linuxcnc (specifically qtplasmac) for control. Freecad has a 
postprocessor for milling operations and this modified postprocessor was based 
on that. Qtplasmac takes over the z moves (probe metal - retract to torch start
height - move to cutting height) so only requires gcode "m3 $0 S1" at start of
each cut (or "m3 $2 S1" for spotting - centerpunching with the plasma cutter - 
I use the drilling operation for this).

For Freecad 0.21 the postprocessor should be placed in path
 - for windows  C:\Program Files\FreeCAD 0.21\Mod\Path\Path\Post\scripts
 - for linux   /usr/lib/freecad/Mod/Path/Post/scripts
   
Process
 - create model in Freecad PartDesign workbench (if the part is sheetmetal with
   bends then you have to unfold in the sheetmetal workbench)
 - in Freecad Path workbench create a path job
   - under the output tab select the postprocessor
   - I have created a 0.045 diameter tool (plasma kerf) so I select that under tools
     (you have to put some value in for feeds and spindle speed to generate gcode
     output but qtplasmac will override these values based on the material selected).

  - now create profile operations
    - under Base geometry add the holes
    - under Operation select the plasma tool that I had added to the Job,
      Cut Side inside and Direction CCW

  - now under Job - Operations there will be Profile right mouse click on this
    and select LeadInOut this will add a Dressup where I deselect the lead out as
    the material has already dropped out so the torch could error out at that point.
    I usually Extend the leadin 0.050 as my torch tends to make a large pierce hole.

    
     
     
