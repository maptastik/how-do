# Exporting a Georeferenced Raster w/ Transparency

OK, so sometimes we're georeferencing old maps or sketch maps that include lots of transparency. Once they're georeferenced and you want to have that saved as a new raster there's the little issue that all that transparency is going to just show up as black. That's no good! Here's how you can get around that in Arc. After the raster is sufficiently georeferenced:

1. In the Georeferencing toolbar navigate to **Georeferencing>Rectify**. Left-click.
2. Set `NoData` to 0
3. Change the `Name` to something cool
4. Leave everything else the same and click Save