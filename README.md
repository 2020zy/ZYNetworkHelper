# ZYNetworkHelper
最好用的IOS网络请求框架最近才上传的
由于缓存采用的是YYcache所以要先导入#YYcache和AFnetworking
# 如果写的不好的地方请指出来，方便修改，希望你们能点亮我的星星，项目里面有我的说明，不懂的可以提出来！！！
# 代码如下

*请求成功的Block
typedef void(^ZYHttpRequestSuccess)(id responseObject);
*请求失败的Block
typedef void(^ZYHttpRequestFailed)(NSError *error);
*缓存的Block
typedef void(^ZYHttpRequestCache)(id responseCache);
*上传或者下载的进度, Progress.completedUnitCount:当前大小 - Progress.totalUnitCount:总大小
typedef void (^ZYHttpProgress)(NSProgress *progress);
*网络状态的Block
typedef void(^ZYNetworkStatus)(ZYNetworkStatusType status);
*有网YES, 无网:NO
+ (BOOL)isNetwork;
*手机网络:YES, 反之:NO
+ (BOOL)isWWANNetwork;
* WiFi网络:YES, 反之:NO
+ (BOOL)isWiFiNetwork;
*取消所有HTTP请求
+ (void)cancelAllRequest;
*实时获取网络状态,通过Block回调实时获取(此方法可多次调用)
+ (void)networkStatusWithBlock:(ZYNetworkStatus)networkStatus;
*取消指定URL的HTTP请求
+ (void)cancelRequestWithURL:(NSString *)URL;
*开启日志打印 (Debug级别)
+ (void)openLog;
*关闭日志打印,默认关闭
+ (void)closeLog;

/**
 *  无缓存
 *
 *  @param URL        请求地址
 *  @param parameters 请求参数
 *  @param requestmode 4种请求方式(get,post,put,deletle)
 *  @param isshowview 是否请求过程中展示界面和动画,具体怎么展示,需要自己去自定义
 *  @param success    请求成功的回调
 *  @param failure    请求失败的回调
 *
 *  @return 返回的对象可取消请求,调用cancel方法
 */
+ (__kindof NSURLSessionTask *)Handle:(NSString *)URL
                        parameters:(id)parameters
                       requestmode:(ZYNetwoker)requestmode
                        isshowview:(BOOL)ison
                           success:(ZYHttpRequestSuccess)success
                           failure:(ZYHttpRequestFailed)failure;
/**
 *  有缓存
 *
 *  @param URL        请求地址
 *  @param parameters 请求参数
 *  @param requestmode 4种请求方式(get,post,put,deletle)
 *  @param isshowview 是否请求过程中展示界面和动画，具体怎么展示，需要自己去自定义
 *  @param responseCache 缓存数据的回调
 *  @param success    请求成功的回调
 *  @param failure    请求失败的回调
 *
 *  @return 返回的对象可取消请求,调用cancel方法
 */
+ (__kindof NSURLSessionTask *)Handle:(NSString *)URL
                        parameters:(id)parameters
                       requestmode:(ZYNetwoker)requestmode
                        isshowview:(BOOL)ison
                           responseCache:(ZYHttpRequestCache)responseCache
                           success:(ZYHttpRequestSuccess)success
                           failure:(ZYHttpRequestFailed)failure;

