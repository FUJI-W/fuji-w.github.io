#### errno 10053

- 报错示例：

  ```shell
  fatal: unable to access 'https://github.com/FUJI-W/dev-renderer/': OpenSSL SSL_read: Connection was aborted, errno 10053
  ```

- 可能原因：

  - Git默认限制推送的大小，运行命令更改限制大小即可

- 解决方法：

  ```shell
  git config --global http.postBuffer 524288000
  ```

  



