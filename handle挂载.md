###handle挂载
handle挂载分为两种方式：
1. 按处理阶段挂载
2. 按需挂载

####按处理阶段
为了精细的控制对客户端请求的处理，nginx把处理过程分成了__11__个阶段，按照顺序依次是
1. NGX_HTTP_POST_READ_PHASE 读取请求内容阶段
2. NGX_HTTP_SERVER_REWRITE_PHASE Server请求地址重写阶段
3. NGX_HTTP_FIND_CONFIG_PHASE 查找配置阶段
4. NGX_HTTP_REWRITE_PHASE Location 请求地址重写阶段
5. NGX_HTTP_PREACCESS_PHASE 访问权限检查准备阶段
6. NGX_HTTP_ACCESS_PHASE 访问权限检查阶段
7. NGX_HTTP_POST_ACCESS_PHASE 访问权限检查提交阶段
8. NGX_HTTP_TRY_FILES_PHASE 配置项try_files处理阶段
9. NGX_HTTP_CONTENT_PHASE 内容产生阶段
10. NGX_HTTP_LOG_PHASE 日志模块处理阶段

一般的情况下，用户自定义的模块都挂载在*NGX_HTTP_CONTENT_PHASE*阶段，挂载的动作一般都在模块上下文指定的**postconfiguration**函数中。

