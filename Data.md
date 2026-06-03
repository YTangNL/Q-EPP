# Individual Patient Data (IPD)

## Kaplan-Meier reconstruction coordinate extraction tables


## Kaplan-Meier reconstruction life table

## Estimate Constant Hazard 
### Revascularization
<img width="1540" height="951" alt="image" src="https://github.com/user-attachments/assets/96fc4849-0632-4806-bc56-81b0364bb0f1" />
> h1_stat
  arm    t_ipd event_ipd        rate
1   0 344620.9       961 0.002788571
2   1 349460.7       757 0.002166195
### Mycardiol Infarction
<img width="1540" height="951" alt="image" src="https://github.com/user-attachments/assets/f5d5f97e-9d42-4853-bd27-c69ca84bcf02" />
> h2_stat
  arm    t_ipd event_ipd        rate
1   0 350370.2       639 0.001823785
2   1 352974.3       465 0.001317376
### Hospitalized Angina
<img width="1540" height="951" alt="image" src="https://github.com/user-attachments/assets/f87af89d-1d1c-4650-b18e-1a6a74f8cf86" />
> h3_stat
  arm    t_ipd event_ipd         rate
1   0 357532.9       241 0.0006740638
2   1 358508.9       239 0.0006666502
### Stroke
<img width="1540" height="951" alt="image" src="https://github.com/user-attachments/assets/830dedf1-38bd-4cc4-836d-7d7cb46aa560" />
> h4_stat
  arm    t_ipd event_ipd         rate
1   0 355959.1       262 0.0007360396
2   1 356221.4       205 0.0005754848
### Cardiovascular Death
<img width="1540" height="951" alt="image" src="https://github.com/user-attachments/assets/4f23c185-07b9-42f2-a207-1cd7c80491bb" />
> h5_stat
  arm    t_ipd event_ipd         rate
1   0 364997.2       238 0.0006520598
2   1 364507.7       251 0.0006885999


# Multi-times-to-events Data

## Uncensored longitudinal Data Wide format
### Data frame: df
> head(df,10)
   id      time1 type1     time2 type2     time3 type3     time4 type4    time5 type5 arm
1   1 120.077012     4 134.03890     5        NA    NA        NA    NA       NA    NA   0
2   2 767.451804     5        NA    NA        NA    NA        NA    NA       NA    NA   0
3   3 489.591816     5        NA    NA        NA    NA        NA    NA       NA    NA   0
4   4   7.598973     1  21.23147     1  45.17234     4  88.22316     5       NA    NA   0
5   5  79.186426     1  99.24298     1 106.97530     1 137.96447     3 149.4664     4   0
6   6 124.257970     1 126.36767     1 126.39688     2 132.41501     1 133.9970     5   0
7   7 260.766187     2 263.74091     1 280.09039     1 293.87279     1 298.4205     1   0
8   8  28.883815     2  48.22941     1  55.02364     2  61.65113     5       NA    NA   0
9   9  84.994311     5        NA    NA        NA    NA        NA    NA       NA    NA   0
10 10 690.731420     2 699.60324     3 710.62273     1 725.19237     1 730.1653     2   0
### Data frame: df_opt
Trancate data: df until 36 months the trial follow up time
> head(df,10)
      id time1 state1 time2 state2 time3 state3 time4 state4 time5 state5   arm ctime
 1     1 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 2     2 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 3     3 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 4     4  7.60      2  21.2      2    36      1    NA     NA    NA     NA     0    36
 5     5 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 6     6 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 7     7 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
 8     8 28.9       3  36        1    NA     NA    NA     NA    NA     NA     0    36
 9     9 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36
10    10 36         1  NA       NA    NA     NA    NA     NA    NA     NA     0    36

## Uncensored longitudinal Data Long format
### Data frame: evo_long
The transition table of evolocumab group, take id:4 as an example
> print(evo_long[evo_long$id == 4,])
      id start  stop status  from    to transition  time transno fromname   toname transname                    
 1     4  0     9.05      0     1     1 1→1         9.05      NA NA         NA     NA                  
 2     4  0     9.05      1     1     2 1→2         9.05       1 Event-free Revasc Event-free -> Revasc
 3     4  0     9.05      0     1     3 1→3         9.05       2 Event-free MI     Event-free -> MI    
 4     4  0     9.05      0     1     4 1→4         9.05       3 Event-free Hosp   Event-free -> Hosp  
 5     4  0     9.05      0     1     5 1→5         9.05       4 Event-free Stroke Event-free -> Stroke
 6     4  0     9.05      0     1     6 1→6         9.05       5 Event-free Death  Event-free -> Death 
 7     4  9.05 14.2       0     2     1 2→1        14.2       NA NA         NA     NA                  
 8     4  9.05 14.2       0     2     2 2→2        14.2       NA NA         NA     NA                  
 9     4  9.05 14.2       0     2     3 2→3        14.2        6 Revasc     MI     Revasc -> MI        
10     4  9.05 14.2       0     2     4 2→4        14.2        7 Revasc     Hosp   Revasc -> Hosp      
11     4  9.05 14.2       0     2     5 2→5        14.2        8 Revasc     Stroke Revasc -> Stroke    
12     4  9.05 14.2       1     2     6 2→6        14.2        9 Revasc     Death  Revasc -> Death
> state_length_evo
           in1        in2        in3        in4        in5       in6
from1 33.88316  0.7611303  0.4296494  0.2583102  0.2086599  0.459090
from2  0.00000 26.9711791  2.3190298  2.0728871  0.4559512  4.180953
from3  0.00000 10.2965437 17.1194050  2.8927080  0.4858941  5.205449
from4  0.00000 14.0273082  2.8145717 15.2014457  0.6310155  3.325659
from5  0.00000  9.5587108  2.6816976  2.8294883 17.1605487  3.769555
from6  0.00000  0.0000000  0.0000000  0.0000000  0.0000000 36.000000
<img width="770" height="475" alt="image" src="https://github.com/user-attachments/assets/366c8041-c805-4dc9-8b98-752e8efd02c0" />

### Data frame: pla_long
The transition table of placebp group, take id:4 as an example
> print(pla_long[pla_long$id == 4,])
      id start  stop status  from    to transition  time transno fromname   toname transname                      
 1     4  0     7.60      0     1     1 1→1         7.60      NA NA         NA     NA                  
 2     4  0     7.60      1     1     2 1→2         7.60       1 Event-free Revasc Event-free -> Revasc
 3     4  0     7.60      0     1     3 1→3         7.60       2 Event-free MI     Event-free -> MI    
 4     4  0     7.60      0     1     4 1→4         7.60       3 Event-free Hosp   Event-free -> Hosp  
 5     4  0     7.60      0     1     5 1→5         7.60       4 Event-free Stroke Event-free -> Stroke
 6     4  0     7.60      0     1     6 1→6         7.60       5 Event-free Death  Event-free -> Death 
 7     4  7.60 21.2       0     2     1 2→1        21.2       NA NA         NA     NA                  
 8     4  7.60 21.2       1     2     2 2→2        21.2       NA NA         NA     NA                  
 9     4  7.60 21.2       0     2     3 2→3        21.2        6 Revasc     MI     Revasc -> MI        
10     4  7.60 21.2       0     2     4 2→4        21.2        7 Revasc     Hosp   Revasc -> Hosp      
11     4  7.60 21.2       0     2     5 2→5        21.2        8 Revasc     Stroke Revasc -> Stroke    
12     4  7.60 21.2       0     2     6 2→6        21.2        9 Revasc     Death  Revasc -> Death     
13     4 21.2  36         1     2     1 2→1        36         NA NA         NA     NA                  
14     4 21.2  36         0     2     2 2→2        36         NA NA         NA     NA                  
15     4 21.2  36         0     2     3 2→3        36          6 Revasc     MI     Revasc -> MI        
16     4 21.2  36         0     2     4 2→4        36          7 Revasc     Hosp   Revasc -> Hosp      
17     4 21.2  36         0     2     5 2→5        36          8 Revasc     Stroke Revasc -> Stroke    
18     4 21.2  36         0     2     6 2→6        36          9 Revasc     Death  Revasc -> Death
> state_length_pla
           in1        in2        in3        in4        in5        in6
from1 33.55047  0.9265153  0.5830267  0.2385771  0.2702335  0.4311736
from2  0.00000 25.4684650  4.2471789  1.3560013  0.8727780  4.0555768
from3  0.00000 10.5132868 18.5713272  1.1694348  0.9683768  4.7775744
from4  0.00000 11.3774144  2.6684016 18.1459522  0.5297023  3.2785295
from5  0.00000  8.7816595  2.9920560  1.2925467 16.3509699  6.5827679
from6  0.00000  0.0000000  0.0000000  0.0000000  0.0000000 36.0000000

<img width="770" height="475" alt="image" src="https://github.com/user-attachments/assets/af33dfb3-1285-4cd0-a884-71d5fb618fc7" />

#### Group state occupation time comparison figure
<img width="770" height="475" alt="image" src="https://github.com/user-attachments/assets/81f2fc6a-9b86-452a-8771-2e290be638d2" />


## Censored longitudinal Data

## QoL weighted RMST
We select interesting id to show the difference between principles, 5 from the Placebo group and 5 from the Evolocumab group
id = 29, 39, 45, 113, 115 (placebo, arm = 0)
id = 4, 25, 35, 99, 170 (Evolocumab, arm = 1)
### Principle 1: Markov Principle
Evolo: 35.22883 months | sd.: 3.41651 
Placebo: 35.19714 months | sd.: 3.407003 
Difference: 0.9509084 days

### Principle 2: Worst-state Update Principle
Evolo: 35.15964 months | sd.: 3.572089 
Placebo: 35.10576 months | sd.: 3.608393 
Difference: 1.61618 days

### Principle 3: Cumulative Product Principle
Evolo: 35.08137 months | sd.: 3.727952 
Placebo: 34.99942 months | sd.: 3.807563 
Difference: 2.458316 days

### Principle 4: RMST (unweighted)
Evolo: 33.88316 months | sd.: 6.826716 
Placebo: 33.55047 months | sd.: 7.27627 
Difference: 9.980595 days


