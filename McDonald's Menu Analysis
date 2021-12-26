!pip install --force-reinstall ibm_db==2.0.8a
!pip install --force-reinstall ibm_db_sa
!pip install sqlalchemy
!pip install ipython-sql

%load_ext sql
%matplotlib inline

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sbn
import ibm_db
import ibm_db_dbi

#hiding username and password for privacy

dsn_hostname = "3883e7e4-18f5-4afe-be8c-fa31c41761d2.bs2io90l08kqb1od8lcg.databases.appdomain.cloud"
dsn_uid = "********"              
dsn_pwd = "****************"     
dsn_driver = "{IBM DB2 ODBC DRIVER}"
dsn_database = "BLUDB"           
dsn_port = "31498"               
dsn_protocol = "TCPIP"            
dsn_security = "SSL"

dsn = (
    "DRIVER={0};"
    "DATABASE={1};"
    "HOSTNAME={2};"
    "PORT={3};"
    "PROTOCOL={4};"
    "UID={5};"
    "PWD={6};"
    "SECURITY={7};").format(dsn_driver, dsn_database, dsn_hostname, dsn_port, dsn_protocol, dsn_uid, dsn_pwd,dsn_security)
print(dsn)

try:
    conn = ibm_db.connect(dsn, "", "")
    print ("Connected to database: ", dsn_database, "as user: ", dsn_uid, "on host: ", dsn_hostname)

except:
    print ("Unable to connect: ", ibm_db.conn_errormsg() )
    
conn = ibm_db.connect(dsn,"********","****************")
pconn = ibm_db_dbi.Connection(conn)
df = pd.read_sql("Select * from MCD_MENU",pconn)

df.describe(include='all')

df.head()

#Enter the name of the food component for scatterplot analysis(replace the y component in UPPERCASE), set as Sodium by default

plot = sbn.swarmplot(x="CATEGORY",y="SODIUM",data=df)
plt.setp(plot.get_xticklabels(),rotation=70)
plt.title("Sodium Content")
plt.show()

#Finding which food item has the maximum amount of the selected component, set as Sodium by default

df.at[df["SODIUM"].idxmax(),'ITEM']

#Using Joint plot analysis to see the correlation between 2 food components, set as Total Fat and Protein by default

plot = sbn.jointplot(x="PROTEIN",y="TOTAL_FAT",data=df)
plot.show()

ibm_db.close(conn)
