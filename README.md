# utl_extending_the_macro_language_with_datastep_arrays_at_macro_execution_time
Extending the macro language with datastep arrays at macro execution time.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Extending the macro language with datastep arrays and sql at macro execution time

    Love the out of the box questions posed in the commercial SAS forum.
    A question is worth a thousand answers.

    github
    https://tinyurl.com/ycqlwwjl
    https://github.com/rogerjdeangelis/utl_extending_the_macro_language_with_datastep_arrays_at_macro_execution_time

    inspired by
    https://communities.sas.com/t5/Base-SAS-Programming/How-to-output-macro-value-to-a-data-set/m-p/463496

    SOAPBOX ON
    I hope SAS does not disable this functionality in the future like it did with SAS scripting in all
    of its enhanced editors?
    You won't find this kind of solution on the commercial SAS forum.
    Incorporating this functionality is not easy and negatively impacts SAS forum favorites,
    call execute, fcmp, run macro, DS2 and macro language.
    I hope others are using it, at least for adhoc work.
    We need better documentation and common, equivalence, pass by reference and pass by value
    enhancements.
    SOAPBOX OFF

    Problem how can I create a dataset and macro variables with sums
    and sums of squares using a new macro array technique.

    SAS Forum: How to output macro value to a data set?

    Summing the elememnts of a an array at macro execution time;

    Note datastap array operating on an array of macro variables and then proc sql
    at macro execution time.

    %symdel x sab / nowarn;

    %macro outDat(a,b);

      * additional macro code?;

      %let rc=%sysfunc(dosubl('
          data ab;
             retain sab 0;
             * more flexible macro array?;
             array ab[2] (&a &b);
             x=sum(of ab[*]);
             call symputx("x",x);
             output;
             sab=0;
             do i=1 to dim(ab);
               sab=sab+ab[i]**2;
             end;
             output;
             put sab=;
             call symputx("sab",sab);
             drop i ;
          run;quit;
          * SQL at macro execution time;
          proc sql;
            select * from ab
          ;quit;
      '));

      %put &=x;
      %put &=sab;

    %mend outDat;

    %outDat(1,2);
