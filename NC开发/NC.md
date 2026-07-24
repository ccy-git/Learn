# NC 

## 元数据建模

    业务对象
       |
    元数据实体
       |
      字段
       |
      VO
       |
    单据界面

- 先定义业务对象结构，再由元数据驱动VO、界面、参照、查询和业务流程

## 实现接口
- 主子表需要实现审批流的接口
  - IBDObject
  - IBillNo  单据号的接口
  - IAuditInfo   创建人 创建时间 修改人 修改时间
  - IOrgInfo     组织信息，限制权限，业务单据尽可能加上
  - IFlowBizItf  
  - businInterface   单据主子VO查询，支持审批流需要实现
  - IPfBillLock   防止并发

##　方法调用
    
        界面xml
           |
         proxy
           |
         接口类
           |
        接口实现类  -- 继承父类  父类实现公共逻辑
           |
         调用BP流程引擎（审批场景）
           |
        数据库操作

## 如何设置自定义参照呢？？


## oracle导入数据
    - 泵
        impdp nc65_jjy/a@orcl DIRECTORY=DATA_PUMP_DIR DUMPFILE=NC65_JJY.DMP REMAP_SCHEMA=NC65_JJY:nc65_jjy
## 单表档案开发
    - 功能注册增加目录
    - 菜单注册增加目录和功能名称
    - 创建元数据实体、实现接口
    - 新建 - 其他 - 单表档案节点 
        - 关联对应功能节点编码
        - 下一步 下一步 。。。 
    - 生成实体代码
    - 生成数据库建表语句和Java代码
    - 添加职责
    - 重启项目

##　前端

###　分隔符
```xml
    <bean id="separatorAction" class="nc.funcnode.ui.action.SeparatorAction" />
```

### 预览
```xml
    <bean id="metDataBasePrintAction" class="nc.ui.pubapp.uif2app.actions.MetaDataBasedPrintAction">
        <property name="model"><ref bean="batchModel"/></property>
        <property name="actioncode" value="Preview"/>
        <property name="actionname" value="预览" />
        <property name="preview" value="true" />
        <property name="nodeKey" value="ot" />
        <property name="exceptionHandler">
            <ref bean="exceptionHandler" />
        </property>
    </bean>
```

### 输出
```xml
    <bean id="metaDataBaseOutPrint" class="nc.ui.pubapp.uif2app.actions.OutputAction">
        <property name="model"><ref bean="batchModel"/></property>
        <property name="actioncode" value="OutPrint"/>
        <property name="actionname" value="输出" />
        <property name="preview" value="false" />
        <property name="nodeKey" value="ot" />
        <property name="exceptionHandler"><ref bean="exceptionHandler" /></property>
    </bean>
```

### 下拉
```xml
<!--    下拉-->
    <bean id="printDownAction" class="nc.funcnode.ui.action.MenuAction">
        <property name="code" value="PrintDown"/>
        <property name="name" value="打印"/>
        <property name="actions">
            <list>
                <ref bean="metaDataBasePreviewAction"/>
                <ref bean="metaDataBasePrintAction"/>
                <ref bean="metaDataBaseOutPrint"/>
            </list>
        </property>
    </bean>
```



