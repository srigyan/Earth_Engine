var imageCollection = ee.ImageCollection("COPERNICUS/S1_GRD"),
    lake = /* color: #d63000 */ee.Geometry.Polygon(
        [[[78.36441874254494, 32.811650794801764],
          [78.35823893297463, 32.8260770144181],
          [78.34313273180275, 32.83126987998513],
          [78.32733988512307, 32.839347067297744],
          [78.32596659410744, 32.85376878822563],
          [78.33832621324807, 32.858960034014146],
          [78.33832621324807, 32.86818816530831],
          [78.3403861497715, 32.87972197904827],
          [78.34862589586525, 32.88721815326],
          [78.34313273180275, 32.91316155161087],
          [78.33557963121682, 32.93506339083176],
          [78.33077311266213, 32.943707361196395],
          [78.32527994859963, 32.963297232223205],
          [78.30124735582619, 32.98518665487377],
          [78.26554178941994, 33.007646472492524],
          [78.27240824449807, 32.98230677766798],
          [78.27858805406838, 32.96905813260402],
          [78.27378153551369, 32.95984051167595],
          [78.28064799059182, 32.94024987444125],
          [78.290947673209, 32.92353678280277],
          [78.28614115465432, 32.874531948557376],
          [78.30262064684182, 32.82838499215674],
          [78.31154703844338, 32.80299393869985],
          [78.35617899645119, 32.79779942033948]]]);

var start_date = ee.Date('2016-01-01');
var finish_date = ee.Date('2022-12-31');

var study_area = lake;

var sentinel = ee.ImageCollection('COPERNICUS/S1_GRD')
    .filterDate(start_date, finish_date)
    //.filter(ee.Filter.calendarRange(12, 3, 'month'))
    .filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VV'))
    //.filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VH'))
    //.filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VH'))
    .filter(ee.Filter.eq('instrumentMode', 'IW'))
    .filterBounds(study_area);
    // .map(function(img) {
    //   return img.clip(study_area);
    // });

print(sentinel)

// Combine the mean and standard deviation reducers.
var reducers = ee.Reducer.mean().combine({
    reducer2: ee.Reducer.median(),
    sharedInputs: true
});



//Seperate ascending and descending orbit images into distinct collections.
// var sentiAsc = sentinel.filter(
//   ee.filter.eq('orbitProperties_pass','ASCENDING'));
// var sentiDesc = sentinel.filter(
//   ee.filter.eq('orbitProperties_pass','DESCENDING'));
  
  
var bands = sentinel.select('VV');


//changing geometry to features 
var lake1=ee.Feature(
  lake,
  {label: 'lake', value:0});

//plotting curve
var chart1=
    ui.Chart.image.series({
      imageCollection: bands, region: lake, reducer: reducers,
      //xproperty: 'systemtime_start'
    })
    .setSeriesNames(['VV', 'VV_median'])
    .setOptions({
      title: 'Tso Moriri Lake',
      hAxis: {title: 'Date', titleTextStyle:{italic:false, bold:true}},
      vAxis: {title: 'Sigma naught (dB)', titleTextStyle: {italic:false, bold:true}},
      lineWidth: 3, colors: ['e37d05', '1d6b99'], curveType:'function'});
print(chart1);
    


// var sent1_chart= ui.Chart.image.series({
//   imageCollection: sentinel1_coll.first(),
//   region: study_area,
//   reducer: ee.Reducer.mean(),
//   scale: 10
// }).setOptions({
//   title: 'Sentinel1',
//   pointSize: 4,
//   lineWidth: 1
// });
// print(sent1_chart);

// var sentinel1_coll= sentinel.first()
// Map.addLayer(sentinel1_coll)
// var sent1_chart= ui.Chart.image.series({
//   imageCollection: sentinel1_coll,
//   region: study_area,
//   reducer: ee.Reducer.mean(),
//   scale: 25
// }).setOptions({title: 'Sentinel1',
//   pointSize: 4,
//   lineWidth: 1
// });
// print( sent1_chart);
