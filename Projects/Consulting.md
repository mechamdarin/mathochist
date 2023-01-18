---
title: "Statistical Consultation"
output: 
  html_document:
    theme: cosmo
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
---




# Findings

Based on the cash prices from June 3, 2019 to May 29, 2020, there is sufficient evidence to conclude that the time of year has an effect on wheat price. There is also sufficient evidence to conclude that the commodity has an effect on price. This makes sense considering that Spring wheat almost always has a higher price than that of Winter wheat. Furthermore, there is sufficient evidence to conclude that the interaction of season and commodity have an effect on price. Conclusion: there *is* a best time to sell wheat. According to the data that was examined, the best average prices can be found in Spring for HRW and Winter for DNS. Those prices are **4.96** and **5.47** respectively (both amounts were rounded to the nearest cent). Since the averages for each commodity/time of year combination were calculated, the *worst* time of year to sell could also be identified. For this dataset, the worst time of year to sell was Summer for both commodities. In a way, this makes sense considering the volatility of the market during harvest time. The averages for this time were **4.78** (DNS) and **4.25** (HRW).   




# Graphic

The following graphic will show the various distributions of price based on commodity and season. From this plot, it can be seen that the cash price has the largest range during the summer months for both commodities. Additionally, this plot can show the best times to sell wheat.



The boxplot showcases a 5 number summary. Five number summaries include the following:

* Minimum - the smallest number of the dataset 

* Quartile 1 - 25% of the data is less than or equal to this point (first edge of the box)

* Median - this is the middle of the dataset if the data were to be put in order (black line in middle)

*50% of the data is less than or equal to the median in most cases*

* Quartile 3 - 75% of the data is less than or equal to this point (second edge of box)

* Maximum - the largest number of the dataset




This plot also has a line drawn across it which shows the overall average of **$4.92**


```r
palette(c("khaki", "goldenrod"))
boxplot(Price ~ Commodity + Season, data = wheat, col = palette(), xlab = "Season", main = "Price Comparison based on Commodity and Season", xaxt = 'n') 
axis(1, at=c(1.5, 3.5, 5.5, 7.5), labels=c("Fall", "Spring", "Summer", "Winter"))
abline(v=c(2.5,4.5,6.5), lty=1, col="gray83")
abline(h = mean(wheat$Price), lty = 2, col = "gray44")
legend("topright", legend = c("DNS", "HRW"), bty = "n", pch = 16, col = palette())
```

![](Consulting_files/figure-html/unnamed-chunk-2-1.png)<!-- -->



```r
pander(favstats(Price ~ Commodity + Season, data = wheat)[,-10][,-9])
```


---------------------------------------------------------------------------
 Commodity.Season   min     Q1     median    Q3     max    mean      sd    
------------------ ------ ------- -------- ------- ------ ------- ---------
     DNS.FALL       4.98   5.14    5.255    5.372   5.54   5.252   0.1518  

     HRW.FALL       4.09   4.36    4.515    4.643   4.97   4.493   0.2142  

    DNS.SPRING      5.05   5.19    5.305    5.478   5.68   5.331   0.1796  

    HRW.SPRING      4.52   4.875    4.95    5.08    5.27   4.955   0.1722  

    DNS.SUMMER      4.3    4.63     4.82    4.915   5.23   4.778   0.2253  

    HRW.SUMMER      3.67   3.92     4.17    4.56    4.94   4.249   0.3652  

    DNS.WINTER      5.28   5.39     5.48    5.56    5.64   5.472   0.09383 

    HRW.WINTER      4.57   4.73     4.83    4.95    5.06   4.834   0.1254  
---------------------------------------------------------------------------


# Data

```r
datatable(wheat, options = list(lengthMenu = c(3, 10, 30)))
```

```{=html}
<div class="datatables html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-edcd28c8e1b931a74d8e" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-edcd28c8e1b931a74d8e">{"x":{"filter":"none","vertical":false,"data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142","143","144","145","146","147","148","149","150","151","152","153","154","155","156","157","158","159","160","161","162","163","164","165","166","167","168","169","170","171","172","173","174","175","176","177","178","179","180","181","182","183","184","185","186","187","188","189","190","191","192","193","194","195","196","197","198","199","200","201","202","203","204","205","206","207","208","209","210","211","212","213","214","215","216","217","218","219","220","221","222","223","224","225","226","227","228","229","230","231","232","233","234","235","236","237","238","239","240","241","242","243","244","245","246","247","248","249","250","251","252","253","254","255","256","257","258","259","260","261","262","263","264","265","266","267","268","269","270","271","272","273","274","275","276","277","278","279","280","281","282","283","284","285","286","287","288","289","290","291","292","293","294","295","296","297","298","299","300","301","302","303","304","305","306","307","308","309","310","311","312","313","314","315","316","317","318","319","320","321","322","323","324","325","326","327","328","329","330","331","332","333","334","335","336","337","338","339","340","341","342","343","344","345","346","347","348","349","350","351","352","353","354","355","356","357","358","359","360","361","362","363","364","365","366","367","368","369","370","371","372","373","374","375","376","377","378","379","380","381","382","383","384","385","386","387","388","389","390","391","392","393","394","395","396","397","398","399","400","401","402","403","404","405","406","407","408","409","410","411","412","413","414","415","416","417","418","419","420","421","422","423","424","425","426","427","428","429","430","431","432","433","434","435","436","437","438","439","440","441","442","443","444","445","446","447","448","449","450","451","452","453","454","455","456","457","458","459","460","461","462","463","464","465","466","467","468","469","470","471","472","473","474","475","476","477","478","479","480","481","482","483","484","485","486","487","488","489","490","491","492","493","494","495","496","497","498","499","500"],["3-Jun-19","3-Jun-19","4-Jun-19","4-Jun-19","5-Jun-19","5-Jun-19","6-Jun-19","6-Jun-19","7-Jun-19","7-Jun-19","10-Jun-19","10-Jun-19","11-Jun-19","11-Jun-19","12-Jun-19","12-Jun-19","13-Jun-19","13-Jun-19","14-Jun-19","14-Jun-19","17-Jun-19","17-Jun-19","18-Jun-19","18-Jun-19","19-Jun-19","19-Jun-19","20-Jun-19","20-Jun-19","21-Jun-19","21-Jun-19","24-Jun-19","24-Jun-19","25-Jun-19","25-Jun-19","26-Jun-19","26-Jun-19","27-Jun-19","27-Jun-19","28-Jun-19","28-Jun-19","1-Jul-19","1-Jul-19","2-Jul-19","2-Jul-19","3-Jul-19","3-Jul-19","5-Jul-19","5-Jul-19","8-Jul-19","8-Jul-19","9-Jul-19","9-Jul-19","10-Jul-19","10-Jul-19","11-Jul-19","11-Jul-19","12-Jul-19","12-Jul-19","15-Jul-19","15-Jul-19","16-Jul-19","16-Jul-19","17-Jul-19","17-Jul-19","19-Jul-19","19-Jul-19","22-Jul-19","22-Jul-19","23-Jul-19","23-Jul-19","24-Jul-19","24-Jul-19","25-Jul-19","25-Jul-19","26-Jul-19","26-Jul-19","29-Jul-19","29-Jul-19","30-Jul-19","30-Jul-19","31-Jul-19","31-Jul-19","1-Aug-19","1-Aug-19","2-Aug-19","2-Aug-19","5-Aug-19","5-Aug-19","6-Aug-19","6-Aug-19","7-Aug-19","7-Aug-19","8-Aug-19","8-Aug-19","9-Aug-19","9-Aug-19","12-Aug-19","12-Aug-19","13-Aug-19","13-Aug-19","14-Aug-19","14-Aug-19","15-Aug-19","15-Aug-19","16-Aug-19","16-Aug-19","19-Aug-19","19-Aug-19","20-Aug-19","20-Aug-19","21-Aug-19","21-Aug-19","22-Aug-19","22-Aug-19","23-Aug-19","23-Aug-19","26-Aug-19","26-Aug-19","27-Aug-19","27-Aug-19","28-Aug-19","28-Aug-19","29-Aug-19","29-Aug-19","30-Aug-19","30-Aug-19","3-Sep-19","3-Sep-19","4-Sep-19","4-Sep-19","5-Sep-19","5-Sep-19","6-Sep-19","6-Sep-19","9-Sep-19","9-Sep-19","10-Sep-19","10-Sep-19","11-Sep-19","11-Sep-19","12-Sep-19","12-Sep-19","13-Sep-19","13-Sep-19","16-Sep-19","16-Sep-19","17-Sep-19","17-Sep-19","18-Sep-19","18-Sep-19","19-Sep-19","19-Sep-19","20-Sep-19","20-Sep-19","23-Sep-19","23-Sep-19","24-Sep-19","24-Sep-19","25-Sep-19","25-Sep-19","26-Sep-19","26-Sep-19","27-Sep-19","27-Sep-19","30-Sep-19","30-Sep-19","1-Oct-19","1-Oct-19","2-Oct-19","2-Oct-19","3-Oct-19","3-Oct-19","4-Oct-19","4-Oct-19","7-Oct-19","7-Oct-19","8-Oct-19","8-Oct-19","9-Oct-19","9-Oct-19","10-Oct-19","10-Oct-19","11-Oct-19","11-Oct-19","14-Oct-19","14-Oct-19","15-Oct-19","15-Oct-19","16-Oct-19","16-Oct-19","17-Oct-19","17-Oct-19","18-Oct-19","18-Oct-19","21-Oct-19","21-Oct-19","22-Oct-19","22-Oct-19","23-Oct-19","23-Oct-19","24-Oct-19","24-Oct-19","25-Oct-19","25-Oct-19","28-Oct-19","28-Oct-19","29-Oct-19","29-Oct-19","30-Oct-19","30-Oct-19","31-Oct-19","31-Oct-19","1-Nov-19","1-Nov-19","4-Nov-19","4-Nov-19","5-Nov-19","5-Nov-19","6-Nov-19","6-Nov-19","7-Nov-19","7-Nov-19","8-Nov-19","8-Nov-19","11-Nov-19","11-Nov-19","12-Nov-19","12-Nov-19","13-Nov-19","13-Nov-19","14-Nov-19","14-Nov-19","15-Nov-19","15-Nov-19","18-Nov-19","18-Nov-19","19-Nov-19","19-Nov-19","20-Nov-19","20-Nov-19","21-Nov-19","21-Nov-19","22-Nov-19","22-Nov-19","25-Nov-19","25-Nov-19","26-Nov-19","26-Nov-19","27-Nov-19","27-Nov-19","29-Nov-19","29-Nov-19","2-Dec-19","2-Dec-19","3-Dec-19","3-Dec-19","4-Dec-19","4-Dec-19","5-Dec-19","5-Dec-19","6-Dec-19","6-Dec-19","9-Dec-19","9-Dec-19","10-Dec-19","10-Dec-19","11-Dec-19","11-Dec-19","12-Dec-19","12-Dec-19","13-Dec-19","13-Dec-19","16-Dec-19","16-Dec-19","17-Dec-19","17-Dec-19","18-Dec-19","18-Dec-19","19-Dec-19","19-Dec-19","20-Dec-19","20-Dec-19","23-Dec-19","23-Dec-19","24-Dec-19","24-Dec-19","26-Dec-19","26-Dec-19","27-Dec-19","27-Dec-19","30-Dec-19","30-Dec-19","31-Dec-19","31-Dec-19","2-Jan-20","2-Jan-20","3-Jan-20","3-Jan-20","6-Jan-20","6-Jan-20","7-Jan-20","7-Jan-20","8-Jan-20","8-Jan-20","9-Jan-20","9-Jan-20","10-Jan-20","10-Jan-20","13-Jan-20","13-Jan-20","14-Jan-20","14-Jan-20","15-Jan-20","15-Jan-20","16-Jan-20","16-Jan-20","17-Jan-20","17-Jan-20","21-Jan-20","21-Jan-20","22-Jan-20","22-Jan-20","23-Jan-20","23-Jan-20","24-Jan-20","24-Jan-20","27-Jan-20","27-Jan-20","28-Jan-20","28-Jan-20","29-Jan-20","29-Jan-20","30-Jan-20","30-Jan-20","31-Jan-20","31-Jan-20","3-Feb-20","3-Feb-20","4-Feb-20","4-Feb-20","5-Feb-20","5-Feb-20","6-Feb-20","6-Feb-20","7-Feb-20","7-Feb-20","10-Feb-20","10-Feb-20","11-Feb-20","11-Feb-20","12-Feb-20","12-Feb-20","13-Feb-20","13-Feb-20","14-Feb-20","14-Feb-20","18-Feb-20","18-Feb-20","19-Feb-20","19-Feb-20","20-Feb-20","20-Feb-20","21-Feb-20","21-Feb-20","24-Feb-20","24-Feb-20","25-Feb-20","25-Feb-20","26-Feb-20","26-Feb-20","27-Feb-20","27-Feb-20","28-Feb-20","28-Feb-20","2-Mar-20","2-Mar-20","3-Mar-20","3-Mar-20","4-Mar-20","4-Mar-20","5-Mar-20","5-Mar-20","6-Mar-20","6-Mar-20","9-Mar-20","9-Mar-20","10-Mar-20","10-Mar-20","11-Mar-20","11-Mar-20","12-Mar-20","12-Mar-20","13-Mar-20","13-Mar-20","16-Mar-20","16-Mar-20","17-Mar-20","17-Mar-20","18-Mar-20","18-Mar-20","19-Mar-20","19-Mar-20","20-Mar-20","20-Mar-20","23-Mar-20","23-Mar-20","24-Mar-20","24-Mar-20","25-Mar-20","25-Mar-20","26-Mar-20","26-Mar-20","27-Mar-20","27-Mar-20","30-Mar-20","30-Mar-20","31-Mar-20","31-Mar-20","1-Apr-20","1-Apr-20","2-Apr-20","2-Apr-20","3-Apr-20","3-Apr-20","6-Apr-20","6-Apr-20","7-Apr-20","7-Apr-20","8-Apr-20","8-Apr-20","9-Apr-20","9-Apr-20","13-Apr-20","13-Apr-20","14-Apr-20","14-Apr-20","15-Apr-20","15-Apr-20","16-Apr-20","16-Apr-20","17-Apr-20","17-Apr-20","20-Apr-20","20-Apr-20","21-Apr-20","21-Apr-20","22-Apr-20","22-Apr-20","23-Apr-20","23-Apr-20","24-Apr-20","24-Apr-20","27-Apr-20","27-Apr-20","28-Apr-20","28-Apr-20","29-Apr-20","29-Apr-20","30-Apr-20","30-Apr-20","1-May-20","1-May-20","4-May-20","4-May-20","5-May-20","5-May-20","6-May-20","6-May-20","7-May-20","7-May-20","8-May-20","8-May-20","11-May-20","11-May-20","12-May-20","12-May-20","13-May-20","13-May-20","14-May-20","14-May-20","15-May-20","15-May-20","18-May-20","18-May-20","19-May-20","19-May-20","20-May-20","20-May-20","21-May-20","21-May-20","22-May-20","22-May-20","26-May-20","26-May-20","27-May-20","27-May-20","28-May-20","28-May-20","29-May-20","29-May-20"],["SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","SUMMER","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","FALL","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","WINTER","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING","SPRING"],["HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS","HRW","DNS"],[5.21,5.4,5.03,5.37,4.8,5.24,4.9,5.36,4.84,5.35,4.88,5.35,4.92,5.36,4.97,5.31,5.03,5.33,5.01,5.3,5,5.28,4.9,5.2,4.82,5.1,4.85,5.07,4.77,5.06,4.9,5.15,4.9,5.19,4.94,5.21,4.93,5.23,4.73,5.16,4.56,5.06,4.44,4.98,4.55,5.02,4.57,4.95,4.59,4.94,4.56,4.88,4.58,4.9,4.78,5.03,4.84,5.04,4.66,4.94,4.63,4.92,4.59,4.91,4.57,4.91,4.46,4.83,4.48,4.82,4.56,4.84,4.54,4.85,4.49,4.86,4.53,4.94,4.5,4.9,4.39,4.81,4.15,4.82,4.21,4.85,4.26,4.87,4.18,4.85,4.17,4.84,4.18,4.83,4.17,4.82,3.92,4.72,3.83,4.66,3.84,4.68,3.89,4.65,3.94,4.69,3.91,4.68,3.86,4.67,3.86,4.65,3.93,4.61,3.91,4.61,3.89,4.55,3.92,4.57,3.92,4.5,3.87,4.42,3.82,4.39,3.67,4.3,3.74,4.4,3.83,4.48,3.83,4.4,3.88,4.42,3.93,4.49,3.93,4.48,3.98,4.53,3.94,4.51,4.04,4.7,3.97,4.67,4.04,4.74,4.14,4.81,4.12,4.85,4.11,4.98,4.1,5.05,4.09,5.15,4.18,5.09,4.17,5.18,4.25,5.15,4.26,5.04,4.2,5,4.2,5,4.19,5.07,4.17,5.19,4.25,5.24,4.28,5.22,4.18,5.16,4.34,5.29,4.4,5.48,4.36,5.41,4.4,5.46,4.46,5.48,4.48,5.4,4.4,5.38,4.36,5.4,4.38,5.43,4.44,5.41,4.47,5.37,4.42,5.28,4.44,5.26,4.43,5.24,4.44,5.25,4.56,5.37,4.53,5.3,4.58,5.32,4.57,5.29,4.54,5.24,4.51,5.24,4.52,5.26,4.68,5.32,4.54,5.26,4.52,5.23,4.47,5.14,4.48,5.14,4.55,5.14,4.58,5.12,4.53,5.06,4.56,5.03,4.66,5.09,4.64,5.05,4.58,4.99,4.7,5.05,4.64,5.15,4.71,5.19,4.75,5.21,4.7,5.29,4.66,5.28,4.61,5.29,4.66,5.34,4.65,5.34,4.77,5.39,4.77,5.41,4.97,5.53,4.92,5.54,4.87,5.49,4.85,5.52,4.87,5.47,4.83,5.48,4.85,5.54,4.95,5.58,5,5.64,4.91,5.58,4.97,5.62,4.91,5.59,4.81,5.48,4.83,5.49,4.81,5.47,4.86,5.48,4.96,5.53,5,5.59,4.98,5.56,4.98,5.57,4.97,5.57,4.85,5.51,5,5.61,5.06,5.63,4.98,5.56,5.03,5.56,4.97,5.53,4.97,5.53,4.93,5.48,4.83,5.41,4.82,5.42,4.76,5.39,4.82,5.39,4.83,5.37,4.89,5.41,4.83,5.38,4.88,5.56,4.88,5.54,4.84,5.52,4.87,5.52,4.82,5.47,4.81,5.46,5.01,5.61,4.95,5.57,4.89,5.5,4.84,5.47,4.7,5.35,4.73,5.37,4.7,5.36,4.61,5.28,4.69,5.33,4.73,5.39,4.74,5.45,4.69,5.4,4.62,5.43,4.62,5.46,4.57,5.41,4.7,5.39,4.71,5.33,4.68,5.35,4.67,5.34,4.59,5.35,4.68,5.35,4.82,5.35,4.91,5.45,4.95,5.47,5.15,5.56,5.16,5.61,5.27,5.63,5.13,5.57,5.12,5.63,5.12,5.6,5.19,5.65,5.05,5.55,4.94,5.5,5.02,5.55,5.05,5.57,5.03,5.55,5.08,5.61,5.22,5.63,5.24,5.68,5.13,5.52,5.09,5.45,5,5.37,5.08,5.37,5.25,5.41,5.17,5.31,5.11,5.29,5.06,5.31,4.95,5.25,4.91,5.2,4.95,5.25,4.88,5.18,5.03,5.26,4.94,5.17,4.98,5.19,4.95,5.21,4.88,5.18,4.89,5.12,4.91,5.17,4.86,5.19,4.8,5.22,4.65,5.09,4.62,5.09,4.63,5.07,4.57,5.05,4.52,5.09,4.69,5.21,4.8,5.19,4.7,5.14,4.73,5.18,4.77,5.14,4.9,5.2,4.96,5.26]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Date<\/th>\n      <th>Season<\/th>\n      <th>Commodity<\/th>\n      <th>Price<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"lengthMenu":[3,10,30],"columnDefs":[{"className":"dt-right","targets":4},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>
```

For this dataset:

* Summer - June 21 to September 20 (2019)

* Spring - June 3 to June 20 (2019) and March 19 to May 29 (2020)

* Fall - September 23 to December 20 (2019)

* Winter - December 23 to March 18 (2019-2020)




# Statistical Test

The $\alpha$ level used for this study was **0.05**. Since all of the $p$-values (last column of table) are lower than **0.05**, the conclusions that were made at the beginning of the analysis are supported. 


```r
wheat.aov <- aov(Price ~ Commodity*Season, data = wheat)
pander(summary(wheat.aov), caption = "Results of Two Way ANOVA Test")
```


----------------------------------------------------------------------
        &nbsp;          Df    Sum Sq   Mean Sq   F value     Pr(>F)   
---------------------- ----- -------- --------- --------- ------------
    **Commodity**        1    41.22     41.22     962.1    7.467e-118 

      **Season**         3    33.86     11.29     263.4    6.431e-102 

 **Commodity:Season**    3    2.547    0.8489     19.81    3.859e-12  

    **Residuals**       492   21.08    0.04284     NA          NA     
----------------------------------------------------------------------

Table: Results of Two Way ANOVA Test

