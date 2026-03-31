1. Download **Car_Make_Info.csv** from GitHub
1. Upload to SAS Content --> My Folder
1. Start new flow
1. Drag Car_Make_Info.csv onto the flow canvas, automatic import
1. Click analyze
1. Preview & modify data: 3 columns and 37 rows
1. Add output table work.car_make
1. run
1. Preview car_make, confirm 3 columns and 37 rows
1. Add clean data
1. keep default qkb locale: english united states
1. standardization tab:
   1. enable
   1. select column: website
   1. def: website
   1. column options: replace existing column
1. casing tab:
   1. enable
   1. select column: parent company
   1. def: proper (organiztion)
   1. column options: replace existing column
1. Add output table work.car_make_clean
1. run
1. confirm 3 cols, 37 rows, standardized data
1. save as import car_make_info.flw in my folder
1. Download **Join Car Data.flw** from GitHub
1. Upload to SAS Content --> My Folder
1. open existing flow Join car Data.flw
   1. join sashelp.cars and work.car_make_clean to make cars_info
   1. characterize data based on parent company
   1. branch rows: general motors, ford motor company
   1. pie chart for vehicle type for both branch tables
1. reset sas session (options -> reset sas session), confirm that work library is empty
1. attempt to run join car data, it fails
1. check log: car_make_clean does not exist, so the other tables aren't created, and so on
1. Add a swimlane, rename to Import CAR_MAKE_INFO
1. Drag the flow import car_make_info onto canvas (from sas content -> my folder), subflow appears in flow
1. reorder swimlanes to put import first (highlight in sub order menu, click up arrow to push to top)
1. Save, run
1. review results along the line
   1. query step: joins on make
   1. cars info: includes everything plus two new columns
   1. characterize data: (scroll to bottom) distribution of parent company, biggest one is general motors, then three way tie between ford motor company, toyota motor corporation, and volkswagen group
   1. branch rows: created two sub tables to save cars manufactured by ford motor company and then by general motors
   1. FMC pie chart: note title & footnote, mostly sedans, then suv
   1. GM pie chart: mostly sedans, then suv and trucks
   1. TMC pie chart: mostly sedans, then suv
   1. VG pie chart: mostly sedans, then sports cars