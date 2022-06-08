# Air-Quality-index-Prediction-
## Run


```sh
$ docker-compose up 
```


| App | Link | Username | Password | 
| ------ | ------ | ------ | ------ |
| JupyterLab | http://localhost:8886/ | - | pust2021 | 
| AirFlow-webServer | http://localhost:8087/ | airflow | airflow | 
| pgAdmin| http://localhost:8089/ | admin@admin.com | 1234 |


## Prepare data 
1- Pulling the CSV files from https://raw.githubusercontent.com/HudaAlQadahAir-Quality-index-Prediction-/main/Air-Quality-index_DailyData 


a)  pulling files names
```
    CMD = "curl -s https://raw.githubusercontent.com/HudaAlQadah/Air-Quality-index-Prediction-/main/Air-Quality-index_DailyData | grep -Eo '[0-9-]*.csv' | sort -Vu"
    output = subprocess.check_output(CMD, shell=True)
    List_of_days = output.decode('utf-8').split('\n')
    List_of_days = [line for line in List_of_days if line.strip() != ""]
```
b) get DF of each day , append it to list  them to list 
```
   def Get_DF_i(Day):
    DF_i=None
    import pandas as pd
    try: 
        URL_Day=f'https://raw.githubusercontent.com/HudaAlQadah/Air-Quality-index-Prediction-/main/Air-Quality-index_DailyData/{Day}.csv'
        DF_day=pd.read_csv(URL_Day)
        DF_day['Day']=Day.split('.')[0]
        DF_i=DF_day.reset_index(drop=True)
    except:
        pass
    
    return DF_i
```

# Final Pipeline   
