# purchase order 中的 date_order 的计算 #
## 1： datetime.today() + 订购规则中的lead_days（类型！=Purchase） ##
### 此时：返回值时 date formate （日期格式 ###）
## 2：根据返回值创建需求单，需求单中的时间是 datetime（时间格式）
### 比如：返回值是：2017-01-13，需求单中的时间则为：2017-01-13 00：00：00 ###
### 需求单时间 - 公司的采购提前期 = 计划日期###
## 3：计划日期 - 供应商的 delay时间 = 采购单中的date_order ##