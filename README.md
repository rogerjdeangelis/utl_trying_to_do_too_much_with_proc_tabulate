# utl_trying_to_do_too_much_with_proc_tabulate
Trying to do too much with proc tabulate. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Trying to do too much with proc tabulate

    Original post Proc tabulate,want to delete left column for keyword such as mean median

    Same results with WPS and SAS

    github
    https://github.com/rogerjdeangelis/utl_trying_to_do_too_much_with_proc_tabulate

    see
    https://goo.gl/cBpUq7
    https://communities.sas.com/t5/ODS-and-Base-Reporting/Proc-tabulate-want-to-delete-left-column-for-keyword-such-as/m-p/440267


    INPUT
    =====

     RULES
       Compute these statistics by year

          SCORE_N
          SCORE_MIN
          SCORE_Q1
          SCORE_MEAN
          SCORE_MEDIAN
          SCORE_Q3
          SCORE_MAX
          SCORE_STDDEV

      WORK.HAVE total obs=4

      NAME     SCORE    YEAR

      john       98     2018
      mary       95     2017
      tom       100     2016
      jerry      80     2016


    PROCESS
    =======


       proc summary data=have  missing nway;
       by year notsorted;
       var score;
       output out=havSum
          n=n min=minimum q1=Q1 mean=mean median=median q3= max=maximum std=Stdev;
       run;quit;

       proc transpose data=havSum out=havXpo;
       var n--stdev;
       id year;
       run;quit;

       proc print data=havxpo noobs;
       run;quit;

    OUTPUT
    ======

      _NAME_          _2018    _2017     _2016

      SCORE_N            1        1       2.000
      SCORE_MIN         98       95      80.000
      SCORE_Q1          98       95      80.000
      SCORE_MEAN        98       95      90.000
      SCORE_MEDIAN      98       95      90.000
      SCORE_Q3          98       95     100.000
      SCORE_MAX         98       95     100.000
      SCORE_STDDEV       .        .      14.142

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data have;
       infile datalines delimiter=',';
       input name $ score  year ;
       datalines;
    john,98,2018
    mary,95,2017
    tom,100,2016
    jerry,80,2016
    ;;;;
    run;quit;

    *
     ___  __ _ ___
    / __|/ _` / __|
    \__ \ (_| \__ \
    |___/\__,_|___/

    ;

    proc summary data=have  missing nway;
    by year notsorted;
    var score;
    output out=havSum
       n=n min=minimum q1=Q1 mean=mean median=median q3= max=maximum std=Stdev;
    run;quit;

    proc transpose data=havSum out=havXpo;
    var n--stdev;
    id year;
    run;quit;

    proc print data=havxpo noobs;
    run;quit;

    *
    __      ___ __  ___
    \ \ /\ / / '_ \/ __|
     \ V  V /| |_) \__ \
      \_/\_/ | .__/|___/
             |_|
    ;


    %utl_submit_wps64('
    libname wrk "%sysfunc(pathname(work))";
    proc summary data=wrk.have  missing nway;
    by year notsorted;
    var score;
    output out=havSum
       n=n min=minimum q1=Q1 mean=mean median=median q3= max=maximum std=Stdev;
    run;quit;
    proc transpose data=havSum out=havXpo;
    var n--stdev;
    id year;
    run;quit;
    proc print data=havxpo noobs;
    run;quit;
    ');

