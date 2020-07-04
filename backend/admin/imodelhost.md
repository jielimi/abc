# IModelHost类 {#imodelhost}

在使用imodeljs-backend中的任何类之前，后端必须调用IModelHost.startup。IModelHost初始化imodeljs-backend并捕获后端配置。后端可能需要根据部署参数设置IModelHostConfiguration.cacheDir,后端可能需要设置IModelHostConfiguration.appAssetsDir来标识其自己的资产目录。例如，如果应用程序需要导入它提供的ECSchemas，则将需要它。

示例代码如下:

```
   public static async startupIModelHost(): Promise<void> {
     // The host configuration.
     // The defaults will work for most backends.
     // Here is an example of how the cacheDir property of the host configuration
     // could be set from an environment variable, which could be set by a cloud deployment mechanism.
     let cacheDir = process.env.MY_SERVICE_CACHE_DIR;
     if (cacheDir === undefined) {
       const tempDir = process.env.MY_SERVICE_TMP_DIR || KnownLocations.tmpdir;
       cacheDir = path.join(tempDir, "iModelJs_cache");
     }

     const imHostConfig = new IModelHostConfiguration();
     imHostConfig.cacheDir = cacheDir;

     // Start up IModelHost, supplying the configuration.
     await IModelHost.startup(imHostConfig);
   }
```



