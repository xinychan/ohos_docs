# IUserAuthInterface


## 概述

声明用户认证驱动的API接口。

**Since:**
3.2
**Version:**
1.0
**相关模块:**

[HdfUserAuth](_hdf_user_auth.md)


## 汇总


### Public 成员函数

  | 名称 | 描述 | 
| -------- | -------- |
| [Init](#init)&nbsp;() | 初始化用户认证驱动缓存信息，用于用户认证框架进程启动时初始化信息。&nbsp; | 
| [AddExecutor](#addexecutor)&nbsp;([in]&nbsp;struct&nbsp;[ExecutorRegisterInfo](_executor_register_info.md)&nbsp;info,&nbsp;[out]&nbsp;unsigned&nbsp;long&nbsp;index,&nbsp;[out]&nbsp;unsigned&nbsp;char[]&nbsp;publicKey,&nbsp;[out]&nbsp;unsigned&nbsp;long[]&nbsp;templateIds) | 添加认证执行器来获取认证能力，用于各认证基础服务如口令认证服务等将认证能力对接到用户认证框架。&nbsp; | 
| [DeleteExecutor](#deleteexecutor)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;index) | 删除执行器，用于清理失效的执行器信息。&nbsp; | 
| [OpenSession](#opensession)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[out]&nbsp;unsigned&nbsp;char[]&nbsp;challenge) | 开启一个认证凭据管理会话，用于在请求管理用户认证凭据前获取有效挑战值。&nbsp; | 
| [CloseSession](#closesession)&nbsp;([in]&nbsp;int&nbsp;userId) | 关闭认证凭据管理会话，完成用户认证凭据管理请求处理后，调用该接口使原挑战值失效。&nbsp; | 
| [BeginEnrollment](#beginenrollment)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;authToken,&nbsp;[in]&nbsp;struct&nbsp;[EnrollParam](_enroll_param.md)&nbsp;param,&nbsp;[out]&nbsp;struct&nbsp;[ScheduleInfo](_schedule_info.md)&nbsp;info) | 开始注册用户认证凭据。当注册凭据类型为口令且该用户已经注册了口令凭据时，将会更新口令凭据。&nbsp; | 
| [UpdateEnrollmentResult](#updateenrollmentresult)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;scheduleResult,&nbsp;[out]&nbsp;struct&nbsp;[EnrollResultInfo](_enroll_result_info.md)&nbsp;info) | 更新用户凭据注册结果，完成凭据注册。&nbsp; | 
| [CancelEnrollment](#cancelenrollment)&nbsp;([in]&nbsp;int&nbsp;userId) | 取消注册请求。&nbsp; | 
| [DeleteCredential](#deletecredential)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;unsigned&nbsp;long&nbsp;credentialId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;authToken,&nbsp;[out]&nbsp;struct&nbsp;[CredentialInfo](_credential_info.md)&nbsp;info) | 删除用户凭据信息。&nbsp; | 
| [GetCredential](#getcredential)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;enum&nbsp;[AuthType](_hdf_user_auth.md#authtype)&nbsp;authType,&nbsp;[out]&nbsp;struct&nbsp;[CredentialInfo](_credential_info.md)[]&nbsp;infos) | 查询用户凭据信息。&nbsp; | 
| [GetUserInfo](#getuserinfo)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[out]&nbsp;unsigned&nbsp;long&nbsp;secureUid,&nbsp;[out]&nbsp;enum&nbsp;[PinSubType](_hdf_user_auth.md#pinsubtype)&nbsp;pinSubType,&nbsp;[out]&nbsp;struct&nbsp;[EnrolledInfo](_enrolled_info.md)[]&nbsp;infos) | 查询用户认证相关信息。&nbsp; | 
| [DeleteUser](#deleteuser)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;authToken,&nbsp;[out]&nbsp;struct&nbsp;[CredentialInfo](_credential_info.md)[]&nbsp;deletedInfos) | 删除用户口令认证凭据，在用户IAM系统内删除该用户，该请求由用户触发。&nbsp; | 
| [EnforceDeleteUser](#enforcedeleteuser)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[out]&nbsp;struct&nbsp;[CredentialInfo](_credential_info.md)[]&nbsp;deletedInfos) | 强制删除用户，该请求由系统内管理用户的模块触发。&nbsp; | 
| [BeginAuthentication](#beginauthentication)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId,&nbsp;[in]&nbsp;struct&nbsp;[AuthSolution](_auth_solution.md)&nbsp;param,&nbsp;[out]&nbsp;struct&nbsp;[ScheduleInfo](_schedule_info.md)[]&nbsp;scheduleInfos) | 开始认证用户，并生成认证方案。&nbsp; | 
| [UpdateAuthenticationResult](#updateauthenticationresult)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;scheduleResult,&nbsp;[out]&nbsp;struct&nbsp;[AuthResultInfo](_auth_result_info.md)&nbsp;info) | 更新认证结果，评估认证方案的认证结果。&nbsp; | 
| [CancelAuthentication](#cancelauthentication)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId) | 取消用户认证请求。&nbsp; | 
| [BeginIdentification](#beginidentification)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId,&nbsp;[in]&nbsp;enum&nbsp;[AuthType](_hdf_user_auth.md#authtype)&nbsp;authType,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;challenge,&nbsp;[in]&nbsp;unsigned&nbsp;int&nbsp;executorSensorHint,&nbsp;[out]&nbsp;struct&nbsp;[ScheduleInfo](_schedule_info.md)&nbsp;scheduleInfo) | 开始用户身份识别，并生成识别方案。&nbsp; | 
| [UpdateIdentificationResult](#updateidentificationresult)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId,&nbsp;[in]&nbsp;unsigned&nbsp;char[]&nbsp;scheduleResult,&nbsp;[out]&nbsp;struct&nbsp;[IdentifyResultInfo](_identify_result_info.md)&nbsp;info) | 更新用户身份识别结果，生成身份识别方案的结果。&nbsp; | 
| [CancelIdentification](#cancelidentification)&nbsp;([in]&nbsp;unsigned&nbsp;long&nbsp;contextId) | 取消用户身份识别请求。&nbsp; | 
| [GetAuthTrustLevel](#getauthtrustlevel)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;enum&nbsp;[AuthType](_hdf_user_auth.md#authtype)&nbsp;authType,&nbsp;[out]&nbsp;unsigned&nbsp;int&nbsp;authTrustLevel) | 获取当前认证类型的认证结果可信等级。&nbsp; | 
| [GetValidSolution](#getvalidsolution)&nbsp;([in]&nbsp;int&nbsp;userId,&nbsp;[in]&nbsp;enum&nbsp;[AuthType](_hdf_user_auth.md#authtype)[]&nbsp;authTypes,&nbsp;[in]&nbsp;unsigned&nbsp;int&nbsp;authTrustLevel,&nbsp;[out]&nbsp;enum&nbsp;[AuthType](_hdf_user_auth.md#authtype)[]&nbsp;validTypes) | 获取指定认证结果可信等级下有效的认证方式。&nbsp; | 


## 成员函数说明


### AddExecutor()

  
```
IUserAuthInterface::AddExecutor ([in] struct ExecutorRegisterInfo info, [out] unsigned long index, [out] unsigned char[] publicKey, [out] unsigned long[] templateIds )
```
**描述:**
添加认证执行器来获取认证能力，用于各认证基础服务如口令认证服务等将认证能力对接到用户认证框架。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| info | 执行器注册信息[ExecutorRegisterInfo](_executor_register_info.md)。&nbsp; | 
| index | 用户认证框架的执行器索引。&nbsp; | 
| publicKey | 用户认证框架公钥。&nbsp; | 
| templateIds | 该执行器已注册的模版ID列表。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### BeginAuthentication()

  
```
IUserAuthInterface::BeginAuthentication ([in] unsigned long contextId, [in] struct AuthSolution param, [out] struct ScheduleInfo[] scheduleInfos )
```
**描述:**
开始认证用户，并生成认证方案。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。&nbsp; | 
| param | 认证方案[AuthSolution](_auth_solution.md)。&nbsp; | 
| scheduleInfos | 调度信息[ScheduleInfo](_schedule_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### BeginEnrollment()

  
```
IUserAuthInterface::BeginEnrollment ([in] int userId, [in] unsigned char[] authToken, [in] struct EnrollParam param, [out] struct ScheduleInfo info )
```
**描述:**
开始注册用户认证凭据。当注册凭据类型为口令且该用户已经注册了口令凭据时，将会更新口令凭据。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| authToken | 用户口令认证令牌。&nbsp; | 
| param | 注册凭据参数[EnrollParam](_enroll_param.md)。&nbsp; | 
| info | 调度信息[ScheduleInfo](_schedule_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### BeginIdentification()

  
```
IUserAuthInterface::BeginIdentification ([in] unsigned long contextId, [in] enum AuthType authType, [in] unsigned char[] challenge, [in] unsigned int executorSensorHint, [out] struct ScheduleInfo scheduleInfo )
```
**描述:**
开始用户身份识别，并生成识别方案。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。&nbsp; | 
| authType | 用户身份识别类型AuthType}。&nbsp; | 
| challenge | 随机挑战值，用于生成用户身份识别令牌，防止重放。&nbsp; | 
| executorSensorHint | 执行器传感器提示，用于找到对应认证方式的传感器。&nbsp; | 
| scheduleInfo | 调度信息[ScheduleInfo](_schedule_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### CancelAuthentication()

  
```
IUserAuthInterface::CancelAuthentication ([in] unsigned long contextId)
```
**描述:**
取消用户认证请求。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### CancelEnrollment()

  
```
IUserAuthInterface::CancelEnrollment ([in] int userId)
```
**描述:**
取消注册请求。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### CancelIdentification()

  
```
IUserAuthInterface::CancelIdentification ([in] unsigned long contextId)
```
**描述:**
取消用户身份识别请求。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### CloseSession()

  
```
IUserAuthInterface::CloseSession ([in] int userId)
```
**描述:**
关闭认证凭据管理会话，完成用户认证凭据管理请求处理后，调用该接口使原挑战值失效。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### DeleteCredential()

  
```
IUserAuthInterface::DeleteCredential ([in] int userId, [in] unsigned long credentialId, [in] unsigned char[] authToken, [out] struct CredentialInfo info )
```
**描述:**
删除用户凭据信息。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| credentialId | 凭据ID。&nbsp; | 
| authToken | 用户口令认证令牌。&nbsp; | 
| info | 删除的凭据信息[CredentialInfo](_credential_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### DeleteExecutor()

  
```
IUserAuthInterface::DeleteExecutor ([in] unsigned long index)
```
**描述:**
删除执行器，用于清理失效的执行器信息。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| index | 用户认证框架的执行器索引。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### DeleteUser()

  
```
IUserAuthInterface::DeleteUser ([in] int userId, [in] unsigned char[] authToken, [out] struct CredentialInfo[] deletedInfos )
```
**描述:**
删除用户口令认证凭据，在用户IAM系统内删除该用户，该请求由用户触发。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| authToken | 用户口令认证令牌。&nbsp; | 
| deletedInfos | 删除的凭据信息[CredentialInfo](_credential_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### EnforceDeleteUser()

  
```
IUserAuthInterface::EnforceDeleteUser ([in] int userId, [out] struct CredentialInfo[] deletedInfos )
```
**描述:**
强制删除用户，该请求由系统内管理用户的模块触发。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| deletedInfos | 删除的凭据信息[CredentialInfo](_credential_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### GetAuthTrustLevel()

  
```
IUserAuthInterface::GetAuthTrustLevel ([in] int userId, [in] enum AuthType authType, [out] unsigned int authTrustLevel )
```
**描述:**
获取当前认证类型的认证结果可信等级。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| authType | 认证类型[AuthType](_hdf_user_auth.md#authtype)。&nbsp; | 
| authTrustLevel | 认证结果可信等级。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### GetCredential()

  
```
IUserAuthInterface::GetCredential ([in] int userId, [in] enum AuthType authType, [out] struct CredentialInfo[] infos )
```
**描述:**
查询用户凭据信息。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| authType | 凭据类型[AuthType](_hdf_user_auth.md#authtype)。&nbsp; | 
| infos | 凭据信息[CredentialInfo](_credential_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### GetUserInfo()

  
```
IUserAuthInterface::GetUserInfo ([in] int userId, [out] unsigned long secureUid, [out] enum PinSubType pinSubType, [out] struct EnrolledInfo[] infos )
```
**描述:**
查询用户认证相关信息。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| secureUid | 安全用户ID。&nbsp; | 
| pinSubType | 口令认证子类型[PinSubType](_hdf_user_auth.md#pinsubtype)。&nbsp; | 
| infos | 注册信息[EnrolledInfo](_enrolled_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### GetValidSolution()

  
```
IUserAuthInterface::GetValidSolution ([in] int userId, [in] enum AuthType[] authTypes, [in] unsigned int authTrustLevel, [out] enum AuthType[] validTypes )
```
**描述:**
获取指定认证结果可信等级下有效的认证方式。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| authTypes | 用于筛选的认证方式列表[AuthType](_hdf_user_auth.md#authtype)。&nbsp; | 
| authTrustLevel | 认证结果可信等级。&nbsp; | 
| validTypes | 有效的认证方式列表[AuthType](_hdf_user_auth.md#authtype)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### Init()

  
```
IUserAuthInterface::Init ()
```
**描述:**
初始化用户认证驱动缓存信息，用于用户认证框架进程启动时初始化信息。

**返回:**

0 表示操作成功。

非0 表示操作失败。


### OpenSession()

  
```
IUserAuthInterface::OpenSession ([in] int userId, [out] unsigned char[] challenge )
```
**描述:**
开启一个认证凭据管理会话，用于在请求管理用户认证凭据前获取有效挑战值。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| challenge | 随机挑战值，用于生成用户身份认证令牌。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### UpdateAuthenticationResult()

  
```
IUserAuthInterface::UpdateAuthenticationResult ([in] unsigned long contextId, [in] unsigned char[] scheduleResult, [out] struct AuthResultInfo info )
```
**描述:**
更新认证结果，评估认证方案的认证结果。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。&nbsp; | 
| scheduleResult | 执行器签发的认证结果。&nbsp; | 
| info | 认证结果信息[AuthResultInfo](_auth_result_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### UpdateEnrollmentResult()

  
```
IUserAuthInterface::UpdateEnrollmentResult ([in] int userId, [in] unsigned char[] scheduleResult, [out] struct EnrollResultInfo info )
```
**描述:**
更新用户凭据注册结果，完成凭据注册。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| userId | 用户ID。&nbsp; | 
| scheduleResult | 执行器签发的注册结果。&nbsp; | 
| info | 录入结果信息[EnrollResultInfo](_enroll_result_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。


### UpdateIdentificationResult()

  
```
IUserAuthInterface::UpdateIdentificationResult ([in] unsigned long contextId, [in] unsigned char[] scheduleResult, [out] struct IdentifyResultInfo info )
```
**描述:**
更新用户身份识别结果，生成身份识别方案的结果。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| contextId | 上下文索引。&nbsp; | 
| scheduleResult | 执行器签发的用户身份识别结果。&nbsp; | 
| info | 用户身份识别结果[IdentifyResultInfo](_identify_result_info.md)。 | 

**返回:**

0 表示操作成功。

非0 表示操作失败。
