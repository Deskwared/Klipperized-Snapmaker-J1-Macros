CAO: 30 April '26 @ 1600 USA Central Time.  (As improvements or changes are made, this repo will be routinely updated. Check for latest file releases prior to embarking on a test/implmentation)

- Optimized heating behavior during print starts.
- Optimized load and unload functionality.  Added suite of load and unload options under revised "Filament" menu.  Modified KlipperScreen file to incorporate.

- Optimized start_end_pause functions.  Worked a bit on filament runout, but this needs continued effort to be fully functional. Added and tested autotune_TMC file/function (will require loading proper firmware if other users also want to implement it.)
  - Other known improvements or things in need of work:
       - Filament runout ready for beta testing. Still get some false positives, likely due to short loop duration.
       - ID'd some odd, intermittent behavior occasionally driving multi-second delays between prime line completion and print start in all modes. Seems to present at random, but I think it is related to heating behavior.
       - *Optional* Increase park speed during cancels
         
- Optimized many macros and fixed some buggy functionality.
- Pause/start/resume/cancel appear to be working correctly.
- Added Orca (SnOrca) g-code files and instructions.
- Mirror/Copy/IDEX modes appear to be functioning correctly.
- Fixed error where manually adjusted z-offset was not saved/recalled properly.
- Incorporated prime lines into Orca start code.
- Troubleshot the issue with stealthchopper missing steps on the Y axis.  (Be sure to reduce acceleration, in Orca, to something less than 4000).
- Added example of mandatory file tree (configure your files as the example shows to ensure full functionality).

Big thank you to Franck FG for the foundation upon which many of these are built.  Some macros may still contain a bit of French! Find his repo here: https://github.com/FranckFG62/J1s-Klipper-Macros
Another huge "thank you" to Evil Azrael without whom none of this would have been possible.  Check out his instructions and links here: https://www.reddit.com/r/KlipperOnJ1/comments/1rwouoa/download_installation_guide/

These macros/g-codes are a work in progress and may contain bugs or errors.  The instructions and guides are written to the best of my ability but may contain omissions or errors.  This suite of macros and g-code should provide a solid fountation for functional testing, but I am positive there are still bugs lurking around in there.
