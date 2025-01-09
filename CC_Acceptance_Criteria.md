- ~~The page should display MolstarViewerFrame (MVF) on the right side.~~
- ~~The page should include a drawer component on the left side containing a Form.~~
- The page should have a save button to capture current page state.
- ~~The page can be opened in draft mode and does not persist anything until I save.~~
- If I try to leave the page but there is unsaved progress I should be warned to save before leaving.
- The Form will include the following fields, to load assets:
    1. Select Maps (CC project maps)
    2. ~~EMDB Import (EMDB maps)~~
    3. ~~Select Models (CC project models)~~
    4. ~~PDB Import (PDB models)~~
    5. Ligand import (SMILE)
- ~~Field pre-population will only be required for project assets, which will be fetched trough a
temporary endpoint that will return hardcoded paths.~~
- To select project assets the DftSingleFileSelector should be used from CC components.
- A component should be present that select a public path (EMDB, PDB, SMILE)
- ~~The fields should load project and public paths (EMDB, PDB, SMILE) on selection.~~
- ~~Selecting any assets, should trigger a download event and update the MVF.~~
- ~~Download progress should be visible.~~
- ~~All added entries for any of the fields should be removable individually.~~
- ~~All added entries should be have a button to toggle between their visible/invisible state.~~
- ~~All added entries should have a button to select them to be manipulated.~~
- Adding multiple assets, should if possible, superimpose those assets in the MVF.
- It should be possible to execute to following operations in the MVF:
rotate,
zoom,
turn on/o@,
move,
clip,
select,
select by residue,
color.
For density maps changing iso level thresholding.
- ~~If a sub-selection exists instead of camera movements the selected components of the model will
be manipulated (This is not realistic for all operations so we can leave this to the developer's
discretion).~~
- If I reload the page, or login on a di@erent browser my viewing session should look like when I last
saved it. This includes all loaded assets in the Drawer as well as all the MVF manipulations.
