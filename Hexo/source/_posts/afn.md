---
title: iOS AFN AFNWorking3.x的封装
categories: "Objective-C" #哪个分类下
tags: [iOS,AFN]
description:  #描述
---

# iOS AFN AFNWorking3.x的封装

只是简单的 post 和 上传post 的请求
没有github、cocoChina上的封装好，但是，使用就好，满足需求就可以。

<!--more-->

还有就是 好修改

**由于，我这服务器接口就一个，可以通过参数，改变接口
例如：
请求接口
http://www.baidu.com?interface='API.home.b2c'&.....
服务器操作是后
http://www.baidu.com/API.home.b2c?.......

还有接口所有参数的加密请求的(由于服务器的操作不同，我这个，就没有写)
加密:  http://www.baidu.com/jfosye973423o805843045e932y2
解密:  http://www.baidu.com?interface='API.home.b2c'&.....

下面开始代码

```objc

APIHttp.h文件
#import <Foundation/Foundation.h>
#import "AFNetworking.h"

//上传文件定义属性
@class APIUploadFormData;



@interface APIHttp :AFHTTPSessionManager
/**
 * @author ----------, 16-03-01 12:03:55
 *
 * @brief 请求数据接口，block返回结果
 *
 * @param paramsDict   请求参数(字典)
 * @param successBlock 请成功，以block形式返回
 * @param failureBlock 请求失败，以block形式返回
 * @param showHUD      是否显示 加载的状态【转圈】
 */
+ (void)postReqeustWithParams:(NSDictionary*)paramsDict
              successBlock:(void (^)(id responseObject))successBlock
              failureBlock:(void (^)(NSError * error))failureBlock
                   showHUD:(BOOL)showHUD;
//==============================================================================
//==============================================================================
/**
 * @author ----------, 16-03-01 14:03:59
 *
 * @brief 上传文件并请求接口
 *
 * @param paramsDict   请求参数(字典)
 * @param uploadParams 上传图片到服务器的文件设置
 * @param successBlock 请成功，以block形式返回
 * @param failureBlock 请求失败，以block形式返回
 * @param showHUD      是否显示 加载的状态【转圈】
 */
+ (void)UploadRequestWithParams:(NSDictionary*)paramsDict
            uploadParams:(APIUploadFormData*)uploadParams
            successBlock:(void (^)(id responseObject))successBlock
            failureBlock:(void (^)(NSError * error))failureBlock
                 showHUD:(BOOL)showHUD;
@end

```

===========================================================
APIHttp.m文件
```objc
#import "APIHttp.h"
#import "constant.h"
#import "APIUploadFormData.h"

static APIHttp * _httpAPIClient =nil;

@interface APIHttp()
@property (nonatomic,assign)BOOL networkError;
@end

@implementation APIHttp


+ (void)postReqeustWithParams:(NSDictionary*)paramsDict
                 successBlock:(void (^)(id responseObject))successBlock
                 failureBlock:(void (^)(NSError * error))failureBlock
                      showHUD:(BOOL)showHUD {
    

    /*-------------【转圈】---------------*/
    if(showHUD) {
        
    }
    
    
    
    AFHTTPSessionManager * manager = [AFHTTPSessionManagermanager];
    manager.responseSerializer.acceptableContentTypes = [NSSetsetWithObjects:@"application/json",@"text/json",@"text/html",nil];
    [manager POST:SERVER_URLparameters:paramsDictprogress:^(NSProgress *_Nonnull uploadProgress) {
        //请求、或者下载、加载速度做高级等待动画
    } success:^(NSURLSessionDataTask *_Nonnull task,id _Nullable responseObject) {
        /*---移除转圈--*/
        successBlock(responseObject);
    } failure:^(NSURLSessionDataTask *_Nullable task,NSError *_Nonnull error) {
        /*---移除转圈--*/
        failureBlock(error);
    }];
}


+ (void)UploadRequestWithParams:(NSDictionary*)paramsDict
                   uploadParams:(APIUploadFormData*)uploadParams
                   successBlock:(void (^)(id responseObject))successBlock
                   failureBlock:(void (^)(NSError * error))failureBlock
                        showHUD:(BOOL)showHUD {
    
    /*---------------【转圈】-------------*/
    if(showHUD) {
        
    }
    
    
    AFHTTPSessionManager * manager = [AFHTTPSessionManagermanager];
    manager.responseSerializer.acceptableContentTypes = [NSSetsetWithObjects:@"application/json",@"text/json",@"",nil];
    
    [manager POST:SERVER_URLparameters:paramsDictconstructingBodyWithBlock:^(id<AFMultipartFormData> _Nonnull formData) {
        NSString * mimeType = @"image/png";
        if(uploadParams.mimeType ==MimeTypeJpeg) {
            mimeType = @"image/jpeg";
        }
        [formData appendPartWithFileData:uploadParams.dataname:uploadParams.namefileName:uploadParams.fileNamemimeType:mimeType];
    } progress:^(NSProgress *_Nonnull uploadProgress) {
        //请求、或者下载、加载速度做高级等待动画
    } success:^(NSURLSessionDataTask *_Nonnull task,id _Nullable responseObject) {
        /*---移除转圈--*/
        successBlock(responseObject);
    } failure:^(NSURLSessionDataTask *_Nullable task,NSError *_Nonnull error) {
        /*---移除转圈--*/
        failureBlock(error);
    }];
    
}



+ (instancetype)shareHttpAPIClicent {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _httpAPIClient = [[APIHttpalloc]initWithBaseURL:[NSURLURLWithString:SERVER_URL]];
        _httpAPIClient.securityPolicy = [AFSecurityPolicypolicyWithPinningMode:AFSSLPinningModeNone];
//        _httpAPIClient.requestSerializer.timeoutInterval = 20; //请求20秒内有效//超时设置

    });
    return_httpAPIClient;
}

//监听网络状态
+ (void)startMonitoring
{
    // 1.获得网络监控的管理者
    AFNetworkReachabilityManager *mgr = [AFNetworkReachabilityManagersharedManager];
    // 2.设置网络状态改变后的处理
    [mgr setReachabilityStatusChangeBlock:^(AFNetworkReachabilityStatus status) {
        // 当网络状态改变了, 就会调用这个block
        switch (status)
        {
            caseAFNetworkReachabilityStatusUnknown://未知网络
                //"未知网络"
               _httpAPIClient.networkError =NO;
                break;
            caseAFNetworkReachabilityStatusNotReachable://没有网络(断网)
               _httpAPIClient.networkError =YES;
                break;
            caseAFNetworkReachabilityStatusReachableViaWWAN://手机自带网络
                //手机自带网络"//
                _httpAPIClient.networkError =NO;
                break;
            caseAFNetworkReachabilityStatusReachableViaWiFi:// WIFI
                //"WIFI"
                _httpAPIClient.networkError =NO;
                break;
        }
    }];
    [mgr startMonitoring];
}

//移除请求
+ (void)removeRequestWithParams:(NSDictionary *)paramsDict {
    AFHTTPSessionManager * manager = [AFHTTPSessionManagermanager];
    [manager DELETE:SERVER_URLparameters:paramsDictsuccess:^(NSURLSessionDataTask *_Nonnull task, id _Nullable responseObject) {
        TTLog(@"移除请求成功");
    } failure:^(NSURLSessionDataTask *_Nullable task,NSError *_Nonnull error) {
        TTLog(@"移除请求失败");
    }];
    
}

@end
```

===========================================================

APIUploadFormData.h文件

```objc

////上传文件定义属性
#import <Foundation/Foundation.h>

typedef NS_ENUM(NSInteger, MimeType) {
    MimeTypeNone,
    MimeTypePng,
    MimeTypeJpeg
};

@interface APIUploadFormData : NSObject
@property (nonatomic,strong)NSData   * data;  //图片二进制
@property (nonatomic,copy)  NSString * name;   //上传到服务器那个文件夹
@property (nonatomic,copy)  NSString * fileName;//上传到服务器的文件名
@property (nonatomic,assign) MimeType  mimeType;//上传的文件类型

@end


===========================================================
```
APIUploadFormData.m文件
为空


如果，有不妥的地方，请多多指教

下载地址: http://download.csdn.NET/detail/srxboys/9449768
