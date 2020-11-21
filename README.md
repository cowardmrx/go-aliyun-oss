# golang_aliyunoss

#about golang_aliyunoss

对阿里云oss-golang sdk 进行上传、删除的简单封装，便于使用
上传使用字节流，内自带 *os.File | *multipart.FileHeader 文件类型转字节流，
传递文件路径 例如：./test.png 。测试案例oss_test.go中有不同操作的案例

#install 
go get github.com/soapBubbleCoward/golang_aliyunoss

#example

    var ossClient *AliOssClient
	ossConfig := &AliOssConfig{
		EndPoint: "oss-cn-shenzhen.aliyuncs.com",      //oss公共域名
		AccessKeyId: "",                               //阿里云id
		AccessKeySecret: "",                           //阿里云key
		BucketName: "",                                //桶名
		//Domain:"",                                     //可访问域名 可不用配置 会自动根据EndPoint与BucketName生成
		//OriginalFileName:true                          //使用使用原文件文件名 不配置或设置为false 那么上传至oss的文件名将使用uuid生成的文件名
	}

	ossClient := ossConfig.CreateOssConnect()
    
    //put 方法返回完整的oss 可访问地址
	uri := ossClient.Put("logo/","./File/3HaqWaOzJWD86DDvZD9Pmn9VUEOBOBbuWackGOXb (2).jpeg")
    fmt.Println(uri)

    //HasExists 方法返回一个bool值 true-存在 false-不存在
    isExists := ossClient.HasExists("logo/a82bbd10-bb3f-5744-8843-5ef0d06c3b23.jpeg")
    fmt.Println(isExists)
    
    
    //delete 方法返回一个bool值 true-删除成功 false-删除失败
    isSuccess := ossClient.Delete("logo/a82bbd10-bb3f-5744-8843-5ef0d06c3b23.jpeg")
    fmt.Println(isSuccess)
    
    //deleteMore 方法返回一个bool值 true-删除成功 false-删除失败
    isSuccess := ossClient.DeleteMore([]string{
        "logo/a82bbd10-bb3f-5744-8843-5ef0d06c3b23.jpeg",
        "logo/a82bbd10-bb3f-5744-8843-5ef0d06c3b23.jpeg"
    })
    fmt.Println(isSuccess)
	



