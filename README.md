# Inventory Optimization
import pandas as pd

df_sales = pd.read_excel('/Users/adlnzmnzr/Downloads/Dynamic Inventory Analytics.xlsx', sheet_name = 'Sales Data')

df_sales.isnull()

df_sales.drop(['Unnamed: 8', 'Unnamed: 9', 'Unnamed: 10', 'Unnamed: 11', 'Unnamed: 12'], axis = 1, inplace = True)
df_sales

df_sales['Order Quantity'] = df_sales['Order Quantity'].astype(int)
df_sales['Order Date'] = pd.to_datetime(df_sales['Order Date'])
df_sales['sku_id'].drop_duplicates()

df_sales['avg_sales_per_day'] = df_sales.groupby(['sku_id', 'warehouse_id', 'order_date'])['order_quantity'].transform('mean')
df_sales['max_sales_per_day'] = df_sales.groupby(['sku_id', 'warehouse_id', 'order_date'])['order_quantity'].transform('max')
df_sales
