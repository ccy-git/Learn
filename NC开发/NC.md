# NC 

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
          调用BP  负责业务流程运转
           |
        数据库操作

## 如何设置自定义参照呢？？