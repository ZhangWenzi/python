# python
python 学习
import pymysql
def get_mysql_connection():
    conn = pymysql.connect(
        host='192.168.0.7',
        port=3306,
        user='root',
        password='dev@110',
        database='mandofin_test',
        charset='utf8')
    return conn

"""
 查询所有数据

 参数说明：sql 需要执行的sql语句

 返回值说明：直接返回sql处理结果，异常则返回None
"""
def query(sql):
    # 连接数据库
    conn = get_mysql_connection()

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = conn.cursor()

    try:
        cursor.execute(sql)
        # 使用 fetchone() 方法获取单条数据.
        result = cursor.fetchall()
        return result
    except Exception as e:
        print(e)
        return None
    finally:
        # 关闭光标
        cursor.close()
        # 关闭数据库连接
        conn.close()

print(query('select * from user where id=1001767'))

"""
 查询一条数据
 
 参数说明：table_name 表名
          column_name 需要查找的列名，多列的话用','隔开,所有列的话直接传'*'
          where_cause 需要的where条件
          
 返回值说明：直接返回sql处理结果，异常则返回None
"""
def query_one(table_name, column_name, where_cause=''):

    # 连接数据库
    conn = get_mysql_connection()

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = conn.cursor()

    try:
        # 使用 execute()  方法执行 SQL 查询
        sql = 'select '+column_name+' from ' + table_name
        if len(where_cause) > 0:
            sql = sql + ' where '+where_cause
        cursor.execute(sql)
        # 使用 fetchone() 方法获取单条数据.
        result = cursor.fetchone()
        return result
    except Exception as e:
        print(e)
        return None
    finally:
        # 关闭光标
        cursor.close()
        # 关闭数据库连接
        conn.close()

print(query_one('user','mobile','id=1001767'))

"""
 查询所有数据
 
 参数说明：table_name 表名
          column_name 需要查找的列名，多列的话用','隔开,所有列的话直接传'*'
          where_cause 需要的where条件
          
 返回值说明：直接返回sql处理结果，异常则返回None

"""
def query_all(table_name, column_name, where_cause=''):

    # 连接数据库
    conn = get_mysql_connection()

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = conn.cursor()

    try:
        # 使用 execute()  方法执行 SQL 查询
        sql = 'select '+column_name+' from ' + table_name
        if len(where_cause) > 0:
            sql = sql + ' where '+where_cause
        cursor.execute(sql)
        # 使用 fetchone() 方法获取所有数据.
        result = cursor.fetchall()
        return result
    except Exception as e:
        print(e)
        return None
    finally:
        # 关闭光标
        cursor.close()
        # 关闭数据库连接
        conn.close()
print(query_one('user','idCard','id=1001767'))
