# utl-Using-SAS-to-find-multiple-unique-events-within-any-seven-day
Using SAS to find multiple unique events within any seven day 
    Using SAS to find multiple unique events within any seven day                                                                       
                                                                                                                                        
    github                                                                                                                              
    https://tinyurl.com/yxtysyev                                                                                                        
    https://github.com/rogerjdeangelis/utl-Using-SAS-to-find-multiple-unique-events-within-any-seven-day                                
                                                                                                                                        
    identify any IP (alongside the Account and Date) that has attempted                                                                 
    to log into three or more accounts within any 7 day window.                                                                         
                                                                                                                                        
    This is a great questions with many applications.                                                                                   
                                                                                                                                        
    Consider patients that are taking more than three medications over a 7 day period.                                                  
    Thanks  wylie_ma                                                                                                                    
    https://communities.sas.com/t5/user/viewprofilepage/user-id/341412                                                                  
                                                                                                                                        
    SAS Forum                                                                                                                           
    https://tinyurl.com/y5cz5y7o                                                                                                        
    https://communities.sas.com/t5/SAS-Programming/Using-SAS-to-find-a-streak-of-occurrences-within-any-seven-day/m-p/693230            
                                                                                                                                        
    Solution by CHRISNZ                                                                                                                 
    https://communities.sas.com/t5/user/viewprofilepage/user-id/16961                                                                   
                                                                                                                                        
    data have;                                                                                                                          
    infile cards dsd ;                                                                                                                  
    input IP :$30. Account $ Date :datetime20.;                                                                                         
    format date datetime20.;                                                                                                            
    cards4;                                                                                                                             
    108.950.45, 12345, 01MAY2020:11:39:55                                                                                               
    108.950.45, 54321, 09MAY2020:12:55:22                                                                                               
    108.950.45, 67890, 10MAY2020:03:00:02                                                                                               
    108.950.45, 09876, 11MAY2020:06:14:03                                                                                               
    108.950.45, 45879, 11MAY2020:12:37:35                                                                                               
    108.950.45, 78562, 13MAY2020:13:13:09                                                                                               
    108.950.45, 99998, 23MAY2020:13:13:09                                                                                               
    108.950.45, 99999, 24MAY2020:13:13:09                                                                                               
    108.950.45, 54321, 27MAY2020:07:12:03                                                                                               
    108.950.45, 54686, 29MAY2020:10:00:02                                                                                               
    220.540.40, 45879, 05MAY2020:09:09:15                                                                                               
    220.540.40, 94532, 11MAY2020:03:41:16                                                                                               
    220.540.40, 45879, 11MAY2020:14:00:58                                                                                               
    110.640.35, 54873, 05MAY2020:17:22:01                                                                                               
    110.640.35, 56454, 05MAY2020:19:22:05                                                                                               
    110.640.35, 87654, 20MAY2020:05:14:12                                                                                               
    ;;;;                                                                                                                                
    run;quit;                                                                                                                           
                                                                                                                                        
                                                                                                                                        
     HAVE total obs=16                                                                                                                  
                                                   | RULES                                                                              
          IP        ACCOUNT           DATE         |                                                                                    
                                                   |                                                                                    
      108.950.45     12345     01MAY2020:11:39:55  |                                                                                    
                                                     GROUP1                                                                             
                                                                                                                                        
      108.950.45     54321     09MAY2020:12:55:22  | 09MAY2020:12:55:22                                                                 
      108.950.45     67890     10MAY2020:03:00:02  | 10MAY2020:03:00:02                                                                 
      108.950.45     09876     11MAY2020:06:14:03  | 11MAY2020:06:14:03                                                                 
      108.950.45     45879     11MAY2020:12:37:35  | 11MAY2020:12:37:35                                                                 
      108.950.45     78562     13MAY2020:13:13:09  | 13MAY2020:13:13:09                                                                 
                                                                                                                                        
                                                     GROUP2                                                                             
                                                                                                                                        
      108.950.45     99998     23MAY2020:13:13:09  | 23MAY2020:13:13:09                                                                 
      108.950.45     99999     24MAY2020:13:13:09  | 24MAY2020:13:13:09                                                                 
      108.950.45     54321     27MAY2020:07:12:03  | 27MAY2020:07:12:03                                                                 
      108.950.45     54686     29MAY2020:10:00:02  | 29MAY2020:10:00:02                                                                 
                                                                                                                                        
      220.540.40     45879     05MAY2020:09:09:15  | NONE                                                                               
      220.540.40     94532     11MAY2020:03:41:16  |                                                                                    
      220.540.40     45879     11MAY2020:14:00:58  |                                                                                    
      110.640.35     54873     05MAY2020:17:22:01  |                                                                                    
      110.640.35     56454     05MAY2020:19:22:05  |                                                                                    
      110.640.35     87654     20MAY2020:05:14:12  |                                                                                    
                                                                                                                                        
    /*           _               _                                                                                                      
      ___  _   _| |_ _ __  _   _| |_                                                                                                    
     / _ \| | | | __| `_ \| | | | __|                                                                                                   
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                    
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                   
                    |_|                                                                                                                 
    */                                                                                                                                  
                                                                                                                                        
    THREE_OR_MORE total obs=9                                                                                                           
                                                                                                                                        
          IP        ACCOUNT           DATE           GROUP                                                                              
                                                                                                                                        
      108.950.45     54321     09MAY2020:12:55:22      1                                                                                
      108.950.45     67890     10MAY2020:03:00:02      1                                                                                
      108.950.45     09876     11MAY2020:06:14:03      1                                                                                
      108.950.45     45879     11MAY2020:12:37:35      1                                                                                
      108.950.45     78562     13MAY2020:13:13:09      1                                                                                
                                                                                                                                        
      108.950.45     99998     23MAY2020:13:13:09      2                                                                                
      108.950.45     99999     24MAY2020:13:13:09      2                                                                                
      108.950.45     54321     27MAY2020:07:12:03      2                                                                                
      108.950.45     54686     29MAY2020:10:00:02      2                                                                                
                                                                                                                                        
    /*         _       _   _                                                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                                 
    / __|/ _ \| | | | | __| |/ _ \| `_ \                                                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                               
                                                                                                                                        
    */                                                                                                                                  
                                                                                                                                        
    * Brilliant;                                                                                                                        
                                                                                                                                        
    * remove same login and account occurances;                                                                                         
    proc sql;                                                                                                                           
      create table REMOVE_SAME_ACCT_LOGINS as                                                                                           
      select unique a.*                                                                                                                 
      from HAVE a, HAVE b                                                                                                               
      where a.IP=b.IP                                                                                                                   
        and a.DATE ne b.DATE                                                                                                            
        and -8 < intck('dtday',a.DATE,b.DATE) < 8                                                                                       
      order by a.IP, a.DATE;                                                                                                            
    quit;                                                                                                                               
                                                                                                                                        
    * form groups of three or more diff accounts;                                                                                       
    data DATE_GROUPS;                                                                                                                   
      set REMOVE_SAME_ACCT_LOGINS;                                                                                                      
      by IP;                                                                                                                            
      if intck('dtday',lag(DATE),DATE) > 7 then GROUP+1;                                                                                
      else if first.IP then GROUP+1;                                                                                                    
    run;                                                                                                                                
                                                                                                                                        
    * counts of three or more;                                                                                                          
    proc sql;                                                                                                                           
      create table THREE_OR_MORE as                                                                                                     
      select *                                                                                                                          
      from DATE_GROUPS                                                                                                                  
      group by GROUP                                                                                                                    
      having count(distinct ACCOUNT) > 2                                                                                                
      order by IP, DATE;                                                                                                                
    quit;                                                                                                                               
                                                                                                                                        
                                                                                                                                        
