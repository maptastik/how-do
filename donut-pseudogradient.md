# Imitating gradient from inner edge

This is to try and think through how to use Inkscape to create something like a radial gradient fill for a polygon that has a hole in it. The idea is that the gradient emanates not from a center point, but rather from the edge of the hole. It seems this isn't possible with the gradient tools available in Inkscape, but it is suggested that something like this could be done using Gaussian blur on the fill. It does seem to work well enough, but there are a few more moving parts than I'm used to working with so I need to document.

## Layers

What are the layers for the map project and their contents

- viewport neatline
	- viewport neatline
- study area - clip
	- copy of viewport neatline (pasted in place)
- study area
	- outline of study area
	- copy of viewport neatline (pasted in place)

## Process

1. Create layers (top-bottom)
	- `viewport neatline`
	- `study area - clip`
	- `study area`
2. Move the neatline of the viewport to  `viewport-neatline` if it's not there already
3. Copy the viewport neatline from `viewport-neatline` and paste in place (*ctrl+alt+v*) in 'study area - clip`
4. Repeat Step 3, but paste in place in `study area`
5. In `study area` draw the shape of the study area
	- Note: Freehand (F6) with Smoothing set at ~50-60 seems to be alright
	- Simplify the path (*ctrl-l*) and mess with the node handles to clean up the shape.
6. In `study area` there are now two (2) objects: An area the size and shape of the viewport and, within that, an area that is the study area. Select both of those shapes and run **Exclusion** on it (*Path>Exclusion; ctrl+^*). The shape of the study area should be a hollow area in the viewport area.
7. If there is a stroke on the shape in `study area`, remove it. 
8. For the shape in `study area`, start with these fill settings:
	- Color: #ffffffff
	- Blur: 4.5
	- Opacity: 95
9. Resize the study area viewport thingy so that the areas around the edges are not hollowed out. The blur will spill over into other parts of the document. Don't worry.
10. Make sure every layer except `study area - clip` and `study area` is locked. Select all and set a clip (*Object>Clip>Set*).
11. This should do it, but if you need to adjust anything, make sure to first release the clip on `study area` (*Object>Clip>Release*)