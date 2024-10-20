# utl-creating-sequences-in-sql-and-linear-interpolation-in-entirely-in-sql-r-and-python
Creating sequences in sql and linear interpolation in entirely in sql r and python  
    %let pgm=utl-creating-sequences-in-sql-and-linear-interpolation-in-entirely-in-sql-r-and-python;

    Creating sequences in sql and linear interpolation in entirely in sql r and python

    github
    https://tinyurl.com/mrudtru8
    https://github.com/rogerjdeangelis/utl-creating-sequences-in-sql-and-linear-interpolation-in-entirely-in-sql-r-and-python

    Pushing the limits od sqllite

        TWO PROBLEMS

              1  create sql sequence table inside sql r and python (without create table clause)

                  table Sequence

                  sequence

                    1.0
                    1.5
                    2.0
                    2.5
                    3.0

              2  r and python sql intepolation

                   INPUT     OUTPUT        INPUT        OUTPUT
                 ========  ==========       ====      ===========
                 tym  val  interpolate        n      interpolate
                  1    1      1.0           1.0          1.00
                  2    .      1.5            .           1.25
                  3    .      2.0            .           1.50
                  4    .      2.5            .           1.75
                  5    3      3.0            .           2.00
                                             .           2.25
                                             .           2.50
                                             .           2.75
                                            5.0          3.00


    https://github.com/rogerjdeangelis/utl-impute-missing-values-in-a-arima-timeseries
    https://github.com/rogerjdeangelis/utl-fill-in-gaps-in-time-series-by-groups
    https://github.com/rogerjdeangelis/utl-fill-in-data-between-two-dates-within-by-group-with-non-missing-values-timeseries
    https://github.com/rogerjdeangelis/utl-number-of-shoppers-in-store-every_5-minutes-time-series

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*   _                       _         _        _     _                         |                                         */
    /*  / |   ___ _ __ ___  __ _| |_ ___  | |_ __ _| |__ | | ___                    |                                         */
    /*  | |  / __| `__/ _ \/ _` | __/ _ \ | __/ _` | `_ \| |/ _ \                   |                                         */
    /*  | | | (__| | |  __/ (_| | ||  __/ | || (_| | |_) | |  __/                   |                                         */
    /*  |_|  \___|_|  \___|\__,_|\__\___|  \__\__,_|_.__/|_|\___|                   |                                         */
    /*                                                                              |                                         */
    /*                         |                                                    |                                         */
    /*           INPUT         |       PROCESS  R AND PYTHON                        |    OUTPUT                               */
    /*           ====          |    (note no input table needed)                    |    ======                               */
    /*                         |    =============================                   |                                         */
    /*                         |                                                    |                                         */
    /*       %let tym1 = 1.;   |   with                                             |    sequence                             */
    /*       %let tym2 = 5.;   |    recursive sequence(n) as (                      |                                         */
    /*       %let step = 0.5;  |    (                                               |     sequence                            */
    /*                         |    select                                          |                                         */
    /*                         |       &tym1                                        |       1.0                               */
    /*                         |    union                                           |       1.5                               */
    /*                         |       all                                          |       2.0                               */
    /*                         |    select                                          |       2.5                               */
    /*                         |       n + &step                                    |       3.0                               */
    /*                         |    from                                            |       3.5                               */
    /*                         |       sequence                                     |       4.0                               */
    /*                         |    where                                           |       4.5                               */
    /*                         |       n < &tym2                                    |       5.0                               */
    /*                         |    )                                               |                                         */
    /*                         |    select                                          |                                         */
    /*                         |       n as sequence                                |                                         */
    /*                         |    from                                            |                                         */
    /*                         |        sequence                                    |                                         */
    /*                         |                                                    |                                         */
    /* -----------------------------------------------------------------------------------------------------------------------*/
    /*   ____    _       _                        _       _                         |                                         */
    /*  |___ \  (_)_ __ | |_ ___ _ __ _ _    ___ | | __ _| |_ ___                   |                                         */
    /*    __) | | | `_ \| __/ _ \ `__| `_ \ / _ \| |/ _` | __/ _ \                  |                                         */
    /*   / __/  | | | | | ||  __/ |  | |_) | (_) | | (_| | ||  __/                  |                                         */
    /*  |_____| |_|_| |_|\__\___|_|  | .__/ \___/|_|\__,_|\__\___|                  |                                         */
    /*                               |_|                                            |                                         */
    /*                                                                              |                                         */
    /*           INPUT                 PROCESS  R AND PYTHON                        |   OUTPUT                                */
    /*           =====              (note no input table needed)                    |  =======                                */
    /*                              ============================                    |                                         */
    /*                                                                              |                                         */
    /*       %let tym1 = 1.;       interp <- sqldf("                                |    want                                 */
    /*       %let tym2 = 5.;         with                                           |                                         */
    /*                                recursive interp(n) as (                      |   x  t    interp                        */
    /*       %let step = 0.5;          select                                       |                                         */
    /*                                    &tym1                                     |   1  1.    1.0                          */
    /*       %let val1=1.;             union                                        |   2  .     1.5                          */
    /*       %let val2=3.;                all                                       |   3  .     2.0                          */
    /*                                 select                                       |   4  .     2.5                          */
    /*                                    n + &step                                 |   5  3 0   3.0                          */
    /*       X  T                      from                                         |                                         */
    /*                                    interp                                    |                                         */
    /*       1  1                      where                                        |                                         */
    /*       2  .                         n < &tym2                                 |                                         */
    /*       3  .                      )                                            |                                         */
    /*       4  .                      select                                       |                                         */
    /*       5  3                        n                                          |                                         */
    /*                                 from                                         |                                         */
    /*                                  interp                                      |                                         */
    /*                             ")                                               |                                         */
    /*                             want <- sqldf("                                  |                                         */
    /*                              select                                          |                                         */
    /*                                n                                             |                                         */
    /*                               ,&val1                                         |                                         */
    /*                                 + (n - &tym1)*(&val2 - &val1)/(&tym2-&tym1)  |                                         */
    /*                                 as est from interp                           |                                         */
    /*                                                                              |                                         */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname sd1 "d:/sd1";

    %let tym1 =1.;
    %let tym2 =5.;
    %let step=0.5;

    /*                      _   _                                       _        _        _     _
    / |  _ __   _ __  _   _| |_| |__   ___  _ __     ___ _ __ ___  __ _| |_ ___ | |_ __ _| |__ | | ___
    | | | `__| | `_ \| | | | __| `_ \ / _ \| `_ \   / __| `__/ _ \/ _` | __/ _ \| __/ _` | `_ \| |/ _ \
    | | | |    | |_) | |_| | |_| | | | (_) | | | | | (__| | |  __/ (_| | ||  __/| || (_| | |_) | |  __/
    |_| |_|    | .__/ \__, |\__|_| |_|\___/|_| |_|  \___|_|  \___|\__,_|\__\___| \__\__,_|_.__/|_|\___|
     _ __      |_|    |___/
    | `__|
    | |
    |_|

    */

    %let tym1 =1.;
    %let tym2 =5.;
    %let step=0.5;

    %utl_rbeginx;
    parmcards4;
    library(sqldf)
    source("c:/oto/fn_tosas9x.r")
    sequence <- sqldf("
       with
        recursive sequence(n) as (
         select
            &tym1
         union
            all
         select
            n + &step
         from
            sequence
         where
            n < &tym2
         )
         select
            n as sequence
         from
           sequence
    ")
     sequence
    fn_tosas9x(
          inp    = sequence
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /*           _   _
     _ __  _   _| |_| |__   ___  _ __
    | `_ \| | | | __| `_ \ / _ \| `_ \
    | |_) | |_| | |_| | | | (_) | | | |
    | .__/ \__, |\__|_| |_|\___/|_| |_|
    |_|    |___/
    */

    %let tym1 =1.;
    %let tym2 =5.;
    %let step=0.5;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    qry="WITH RECURSIVE sequence(n) AS ( SELECT &tym1 UNION ALL SELECT n + &step FROM sequence WHERE n < &tym2 ) SELECT n as sequence FROM sequence"
    print(qry)
    want=pdsql(qry)
    print(want)
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx(resolve=Y);

    proc print data=sd1.pywant;
    run;quit;

    /***************************************************************************************************************************/
    /*                                       |                                                                                 */
    /*  ____     ___                         |              _   _                    ___                                       */
    /* |  _ \   ( _ )    ___  __ _ ___       |  _ __  _   _| |_| |__   ___  _ __    ( _ )    ___  __ _ ___                     */
    /* | |_) |  / _ \/\ / __|/ _` / __|      | | `_ \| | | | __| `_ \ / _ \| `_ \   / _ \/\ / __|/ _` / __|                    */
    /* |  _ <  | (_>  < \__ \ (_| \__ \      | | |_) | |_| | |_| | | | (_) | | | | | (_>  < \__ \ (_| \__ \                    */
    /* |_| \_\  \___/\/ |___/\__,_|___/      | | .__/ \__, |\__|_| |_|\___/|_| |_|  \___/\/ |___/\__,_|___/                    */
    /*                                       | |_|    |___/                                                                    */
    /*                                       |                                                                                 */
    /*  R           SAS                      |                                                                                 */
    /*                                       |                                                                                 */
    /*  sequence    ROWNAMES    SEQUENCE     |     sequence      SEQUENCE                                                      */
    /*                                       |                                                                                 */
    /*       1.0        1          1.0       |  0       1.0         1.0                                                        */
    /*       1.5        2          1.5       |  1       1.5         1.5                                                        */
    /*       2.0        3          2.0       |  2       2.0         2.0                                                        */
    /*       2.5        4          2.5       |  3       2.5         2.5                                                        */
    /*       3.0        5          3.0       |  4       3.0         3.0                                                        */
    /*       3.5        6          3.5       |  5       3.5         3.5                                                        */
    /*       4.0        7          4.0       |  6       4.0         4.0                                                        */
    /*       4.5        8          4.5       |  7       4.5         4.5                                                        */
    /*       5.0        9          5.0       |  8       5.0         5.0                                                        */
    /*                                       |                                                                                 */
    /***************************************************************************************************************************/

    /*                  _   _                  _       _                        _       _
     _ __   _ __  _   _| |_| |__   ___  _ __  (_)_ __ | |_ ___ _ __ _ __   ___ | | __ _| |_ ___
    | `__| | `_ \| | | | __| `_ \ / _ \| `_ \ | | `_ \| __/ _ \ `__| `_ \ / _ \| |/ _` | __/ _ \
    | |    | |_) | |_| | |_| | | | (_) | | | || | | | | ||  __/ |  | |_) | (_) | | (_| | ||  __/
    |_|    | .__/ \__, |\__|_| |_|\___/|_| |_||_|_| |_|\__\___|_|  | .__/ \___/|_|\__,_|\__\___|
     _     |_|    |___/  _                                         |_|
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    %let tym1 =1.;   %let val1=1.;
    %let tym2 =5.;   %let val2=3.;
    %let step=0.5;

    /*
     _ __
    | `__|
    | |
    |_|

    */

    proc datasets lib=sd1 nodetails nolist;
      delete rrwant;
    run;quit;

    %let tym1 =1.;   %let val1=1.;
    %let tym2 =5.;   %let val2=3.;
    %let step=0.5;

     %utl_rbeginx;
     parmcards4;
     library(sqldf)
     library(haven)
     source("c:/oto/fn_tosas9x.r")
     interp <- sqldf("
       with
          recursive interp(n) as (
       select
          &tym1
       union
          all
       select
          n + &step
       from
          interp
       where
          n < &tym2
       )
       select
          n
      from
          interp
     ")
     want <- sqldf("
      select
          n
         ,&val1
             + (n - &tym1)*(&val2 - &val1)/(&tym2-&tym1)
             as est
      from interp
     ")
     want;
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rrwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rrwant;
    run;quit;

    /*           _   _
     _ __  _   _| |_| |__   ___  _ __
    | `_ \| | | | __| `_ \ / _ \| `_ \
    | |_) | |_| | |_| | | | (_) | | | |
    | .__/ \__, |\__|_| |_|\___/|_| |_|
    |_|    |___/
    */

    %let tym1 =1.;   %let val1=1.;
    %let tym2 =5.;   %let val2=3.;
    %let step=0.5;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    qry1="with recursive interp(n) as ( select &tym1 union all select n + &step from interp where n < &tym2 ) select n from interp"
    qry2="select n, &val1+ (n - &tym1)*(&val2 - &val1)/(&tym2-&tym1)  as est from interp"
    interp=pdsql(qry1)
    want=pdsql(qry2)
    print(want)
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx(resolve=Y);

    proc print data=sd1.pywant;
    run;quit;



    /***************************************************************************************************************************/
    /*                                       |                                                                                 */
    /*  ____     ___                         |              _   _                    ___                                       */
    /* |  _ \   ( _ )    ___  __ _ ___       |  _ __  _   _| |_| |__   ___  _ __    ( _ )    ___  __ _ ___                     */
    /* | |_) |  / _ \/\ / __|/ _` / __|      | | `_ \| | | | __| `_ \ / _ \| `_ \   / _ \/\ / __|/ _` / __|                    */
    /* |  _ <  | (_>  < \__ \ (_| \__ \      | | |_) | |_| | |_| | | | (_) | | | | | (_>  < \__ \ (_| \__ \                    */
    /* |_| \_\  \___/\/ |___/\__,_|___/      | | .__/ \__, |\__|_| |_|\___/|_| |_|  \___/\/ |___/\__,_|___/                    */
    /*                                       | |_|    |___/                                                                    */
    /*                                       |                                                                                 */
    /*   R            SAS                    | PYTHON         SAS                                                              */
    /*                                       |                                                                                 */
    /*       n  est   ROWNAMES  N      EST   |     n  est       N      EST                                                     */
    /*                                       |                                                                                 */
    /*   1 1.0 1.00       1    1.0    1.00   | 1 1.0 1.00      1.0    1.00                                                     */
    /*   2 1.5 1.25       2    1.5    1.25   | 2 1.5 1.25      1.5    1.25                                                     */
    /*   3 2.0 1.50       3    2.0    1.50   | 3 2.0 1.50      2.0    1.50                                                     */
    /*   4 2.5 1.75       4    2.5    1.75   | 4 2.5 1.75      2.5    1.75                                                     */
    /*   5 3.0 2.00       5    3.0    2.00   | 5 3.0 2.00      3.0    2.00                                                     */
    /*   6 3.5 2.25       6    3.5    2.25   | 6 3.5 2.25      3.5    2.25                                                     */
    /*   7 4.0 2.50       7    4.0    2.50   | 7 4.0 2.50      4.0    2.50                                                     */
    /*   8 4.5 2.75       8    4.5    2.75   | 8 4.5 2.75      4.5    2.75                                                     */
    /*   9 5.0 3.00       9    5.0    3.00   | 9 5.0 3.00      5.0    3.00                                                     */
    /*                                       |                                                                                 */
    /***************************************************************************************************************************/ /

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
