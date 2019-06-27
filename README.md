# utl-transposing-a-complex-data-set-in-sas-arts-transpose-macro
Transposing a complex data set in sas arts transpose macro

    Transposing a complex data set in sas arts transpose macro                                                                 
                                                                                                                               
    No need for two 'slow' transposes, use the very fast and flexible                                                          
    transpose macro by                                                                                                         
                                                                                                                               
    Arthur Tabachneck, Xia Ke Shan, Robert Virgile and Joe Whitehurst                                                          
                                                                                                                               
    The macro is built to easily transpose mutiple sets of variables.                                                          
                                                                                                                               
    github                                                                                                                     
    http://tinyurl.com/yyp6ontd                                                                                                
    https://github.com/rogerjdeangelis/utl-transposing-a-complex-data-set-in-sas-arts-transpose-macro                          
                                                                                                                               
    macros                                                                                                                     
    https://tinyurl.com/y9nfugth                                                                                               
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                 
                                                                                                                               
    StacOverflow                                                                                                               
    https://tinyurl.com/yxka9g8q                                                                                               
    https://stackoverflow.com/questions/56762545/transposing-a-complex-data-set-in-sas                                         
                                                                                                                               
    *_                   _                                                                                                     
    (_)_ __  _ __  _   _| |_                                                                                                   
    | | '_ \| '_ \| | | | __|                                                                                                  
    | | | | | |_) | |_| | |_                                                                                                   
    |_|_| |_| .__/ \__,_|\__|                                                                                                  
            |_|                                                                                                                
    ;                                                                                                                          
                                                                                                                               
    data have;                                                                                                                 
    input id class $ name $ weight lipids plasma lod;                                                                          
    cards4;                                                                                                                    
    1   AAA Lead    1.55    44.0   10.0      5.00                                                                              
    1   AAB Mercury 1.55    222.0  100.0     75.00                                                                             
    2   AAA Lead    1.25    25.5   12.0      5.00                                                                              
    ;;;;                                                                                                                       
    run;                                                                                                                       
                                                                                                                               
    /*                                                                                                                         
     WORK.HAVE total obs=3                                                                                                     
                                                                                                                               
      id    class    name       weight    lipids    plasma    lod                                                              
                                                                                                                               
       1     AAA     Lead        1.55       44.0       10       5                                                              
       1     AAB     Mercury     1.55      222.0      100      75                                                              
       2     AAA     Lead        1.25       25.5       12       5                                                              
    */                                                                                                                         
                                                                                                                               
    *            _               _                                                                                             
      ___  _   _| |_ _ __  _   _| |_                                                                                           
     / _ \| | | | __| '_ \| | | | __|                                                                                          
    | (_) | |_| | |_| |_) | |_| | |_                                                                                           
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                          
                    |_|                                                                                                        
    ;                                                                                                                          
                                                                                                                               
    WANT total obs=2                                                                                                           
                                                                                                                               
                      lipids_    plasma_                lipids_    plasma_      lod_                                           
      id    weight      Lead       Lead     lod_Lead    Mercury    Mercury    Mercury                                          
                                                                                                                               
       1     1.55       44.0        10          5         222        100         75                                            
       2     1.25       25.5        12          5           .          .          .                                            
                                                                                                                               
    *          _       _   _                                                                                                   
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                        
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                       
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                      
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                      
                                                                                                                               
    ;                                                                                                                          
                                                                                                                               
    %utl_transpose(data=have, out=want, by=id weight, id=name,                                                                 
     delimiter=_, var=lipids plasma lod);                                                                                      
                                                                                                                               
                                                                                                                               
