Socioboard Api's is created with Node.js, Express, MongoDB and Sequelize ORM. Socioboard Api are classified to four micro services. They are namely

> User Services - Responsible for Managing User, Team, Payment, App Insights and Admin functionalities.

> Publish Services – Responsible for Managing Media Uploads, Scheduling, Publish now and Report functionalities through respective Social Network Api's.

> Feed Services – Responsible for fetching Feeds from Social network API's and various popular trending networks such as Pixabay, Imgur, Daily motion, Flickr and so on.

> Notification Services – Responsible for sending emails and notify the user activities through Socket.io

---

## `NODE micro services setup :system:`

---

## Pre Requirement

`NODE ^14 OR LATEST`

`NPM ^7 OR LATEST`

`NODEMON ^2 OR LATEST`

`MIN 5 FREE PORTS`

`PM2 – FOR AUTOMATION & EASY MANAGEMENT`

`Mongo Database`

`MySQL Database`

`5 free ports`

## Installation Process

    1. Requirement check.
        a. Node js ^14 (14 or more)
        b. Npm version ^6 (6 or more)
        c. PM2 version (latest)
        d. Nodemon Latest version (2 or more)
        e. MySQL Creds
        f. Mongo Database Creds
    2. Setting up server environment.
    3. Installing Node Packages in all folders
    4. Setting up MySQL Database
    5. Updating the config files (minimum required should fill with proper details)
    6. Starting the micro-services (User, Feeds, Publish, Update)
    7. Checking the Error Logs

## #1. Requirement Check

    a. To check node installed or not, use`node -v` command in Terminal
        It should give version number. like: v14.15.2
        -- If not Please visit the site(https://nodejs.org/) and download the latest stable version.

    b. To check npm version, use`npm -v`.
        It should give version number. like: 7.15.1
        -- It won't work if there's no node version (above one)

    c. To check pm2 installed or not use`pm2 --version`
        It should give version number. like: 5.1.0
        -- If not Please visit the site(https://pm2.keymetrics.io/) and download the latest stable version.
                    or
            use `npm install pm2 -g` command to install the latest stable version.
    d. To check nodemon version, use `nodemon -v`
        It should give version number. like: 2.0.13
        -- If not please use `npm i nodemon -g` to install latest one.
    e. MySQL & Mongo creds are compulsory, so Please follow proper way to install it in local system or use cloud creds.

## #2. Set Environment for NODE

## 1. `Open the Terminal in Root Directory (current folder)`

For windows environment

```code
    set NODE_ENV=development
```

`For linux || mac environment`

```code
    export NODE_ENV=development
```

## #3. Installing Node Packages in all folders

```code
cd ./User && npm install && cd ../Feeds && npm install && cd ../Common && npm install && cd ../Update && npm install && cd ../Publish && npm install && cd ../Notification && npm install
```

## #4. Setting up MySQL Database

    A. Setting the config file for Database connections.

    Open the config.json file located at`socioboard-api\Common\Sequelize-cli\config\config.json`

    And Update The below mentioned keys in`development` key
                        "username": "<< DB USER NAME >>",
                        "database": "<< Database name >>",
                        "password": "<< password >>",
                        "host": "127.0.0.1",
        and save the file.

    B. Creating Tables.
         run`set NODE_ENV=development & npx sequelize-cli db:migrate` command in `socioboard-api\Common\Sequelize-cli`

    or Run this command in root directory.

    `cd socioboard-api\Common\Sequelize-cli & npx sequelize-cli db:migrate`

    It should list all the tables it creating without any errors.

    C. Setting up migrations.
        As you're in the Sequelize-cli folder you can simply run`npx sequelize-cli db:seed --seed 20210303111816-initialize_application_informations.cjs` command.

    It will add data into single table.

## #5. Updating the config files (minimum required should fill with proper details)

    Most important is we need to setup mongo and mysql objects values properly in all config folders.

    Ex: in`User` folder `config/development.json` file and fill the << Description >> places with correct files.

```diff
- Note: In all folders update the configuration files properly.
```

## #6. Generating swagger files in Micro-Services

    Make sure you're in Root directory.

    For Generating swagger file in User micro service you need to go to User folder Then run`npm run swagger` and it should say success.

###### For generating swagger files in all micro-services you need to run the following command

```diff
    cd ./socioboard-api/User & npm run swagger & cd ../Feeds & npm run swagger & cd ../Publish & npm run swagger & cd ../Notification & npm run swagger & cd ../Update & npm run swagger
```

    For Linux

```
    cd ./socioboard-api/User && npm run swagger && cd ../Feeds && npm run swagger && cd ../Publish && npm run swagger && cd ../Notification && npm run swagger && cd ../Update && npm run swagger

```

```diff
+ We should do this in rest 3 micro services as well.
```

## #7. Starting the micro-services

    Make sure you're in Root directory.

    For starting User micro service you need to go to User folder Then run`nodemon user.server.js` and it should start in port 3000(which is configured in `development.json` file)

```diff
+ We should do this in rest 3 micro services as well.
```

### `Note:` If you facing any issue, in that same folder you need to go to resources/Log/ResponseLog folder and check the proper log file to fix it.

### `If you want to run all with pm2`

    Your Terminal should be in Root Directory. then run the below command.

```code
set NODE_ENV=development & cd ./socioboard-api/User & pm2 start ./socioboard-api/User/user.server.js & cd ../Feeds & pm2 start ./socioboard-api/Feeds/feeds.server.js & cd ../Publish & pm2 start ./socioboard-api/Publish/publish.server.js & cd ../Notification & pm2 start ./socioboard-api/Notification/notify.server.js & cd ../Update & pm2 start ./socioboard-api/Update/update.server.js & pm2 status
```

    It will Give you all your services status in a table.

---

---

1. **feed_socioboard, user_socioboard, notification_socioboard**: Cung cấp thông tin cần thiết về host và cổng cho các ứng dụng khác nhau.
2. **session**

   - `name`: Tên của session, đặt theo ứng dụng của bạn.
   - `key_1, key_2`: Đây là chuỗi mật khẩu được sử dụng để mã hóa session. Chuỗi này phải đủ phức tạp để không thể bị tấn công từ điển.
3. **swagger_host_url**: URL host đang chạy API với Swagger.
4. **authorize**

   - `secret, token_secret`: Mật khẩu bảo mật.
   - `algorithm`: Phiên bản thuật toán mã hóa.
   - `encoding_typeOne, encoding_typeTwo`: Tiêu chuẩn mã hóa.
5. **analytics**

   - `tracking_id`: ID theo dõi trên Google Analytics.
   - `view_id`: ID hiển thị của Google Analytics.
   - `ganalytics_service_email`: Email dịch vụ của Google Analytics.
   - `ganalytics_private_key`: Khóa riêng của Google Analytics.
6. **mailService**

   - `defaultMailOption`: Phương thức email được sử dụng mặc định.
   - `sendgrid`, `gmailServices`: Các thông tin cần thiết để cấu hình dịch vụ email tương ứng.
7. **mysq**

   - Cung cấp thông tin liên quan đến cấu hình máy chủ MySQL gồm `host`, `username`, `database`, `password`.
8. **mongo**

   - `username, password, host, db_name`: Thông tin để kết nối với máy chủ MongoDB.
9. **profile_add_redirect_url**: URL chuyển hướng sau khi hồ sơ đã được thêm thành công.
10. **facebook_api, google_api, twitter_api, linkedIn_api, instagram_api, instagram_business_api, pinterest, tumblr_api**

    - Cung cấp thông tin cần thiết để tích hợp với các nền tảng này như `client_id, client_secret`, các URL chuyển hướng, tần suất cập nhật, v.v.
11. **twitter_data**

    - Cung cấp Bearer Token, Access Token và Access Secret từ tài khoản Twitter của bạn.
12. **content_studio**

    - Cung cấp thông tin cần thiết để tích hợp với các nền tảng nội dung khác nhau như Daily Motion, Giphy, News API, Pixabay, Flickr, Imgur, YouTube.
13. **test_url**: URL dự án để kiểm thử.
14. **rssUrl**

    - Đặt số lượt xem lịch sử tối đa.
15. **facebook_api, google_api, twitter_api, linkedIn_api, instagram_api, instagram_business_api, pinterest, tumblr_api**

    - `app_id`, `client_id`: Đây là mã nhận dạng ứng dụng duy nhất mà các nền tảng này cung cấp khi bạn đăng ký ứng dụng của mình trên các nền tảng này.
    - `secret_key`, `client_secrets, client_secret`: Đây là mật khẩu bí mật được sử dụng để giữ an toàn thông tin của bạn khi giao tiếp giữa ứng dụng của bạn và các nền tảng này.
    - `redirect_url, fbprofile_add_redirect_url, login_redirect_url...`: Đây là liên kết mà người dùng sẽ được đưa đến sau khi hoàn thành xác thực thành công trên các nền tảng này.
    - `webhook_token, webhook_url`: Cung cấp cơ sở hạ tầng cần thiết để nhận và xử lý các sự kiện API thời gian thực từ các nền tảng này.
    - `update_time_frequency_value`, `update_time_frequency_factor`: Thiết lập tần suất cập nhật dữ liệu từ các nền tảng này.
16. **content_studio**

    - `daily_motion`: Nền tảng video. Cần cung cấp `api_key`, `secret_key`, `version`, `count` (số lượng video tối đa sẽ truy vấn mỗi lần).
    - `giphy`: Dịch vụ chia sẻ GIF. Cần cung cấp `api_key`, `count` (số lượng GIF tối đa để truy vấn mỗi lần), `version` và `path` (đường dẫn lưu trữ GIF).
    - `newsapi`: Dịch vụ cung cấp tin tức API. Cần cung cấp `api_key`, `count` (số lượng tin tức tối đa để truy vấn mỗi lần) và `version`.
    - `pixabay`: Dịch vụ cung cấp hình ảnh chất lượng. Cần cung cấp `api_key`, `count` (số lượng hình ảnh tối đa để truy vấn mỗi lần), `version` và `path` (đường dẫn lưu trữ hình ảnh).
    - `flickr`: Dịch vụ chia sẻ hình ảnh. Cần cung cấp `api_key`, `api_secret`, `count` (số lượng hình ảnh tối đa để truy vấn mỗi lần), `version` và `path` (đường dẫn lưu trữ hình ảnh).
    - `imgur`: Dịch vụ chia sẻ hình ảnh. Cần cung cấp `client_id`, `client_secret`, `count` (số lượng hình ảnh tối đa để truy vấn mỗi lần), `version` và `path` (đường dẫn lưu trữ hình ảnh).
    - `youtube`: Dịch vụ video của Google. Cần cung cấp `api_key` và `count` (số lượng video tối đa để truy vấn mỗi lần), `version`.

---

**facebook_api**

- `app_id`: ID của ứng dụng Facebook được cung cấp khi bạn đăng ký ứng dụng trên Facebook Developer.
- `secret_key`: Mã khóa bí mật của ứng dụng Facebook.
- `redirect_url`: URL để Facebook chuyển hướng người dùng sau khi hoàn thành quy trình xác thực.
- `fbprofile_add_redirect_url`: URL chuyển hướng khi người dùng thêm một hồ sơ Facebook.
- `webhook_token`: Token được Facebook sử dụng để xác minh webhook của bạn.
- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Facebook.

**google_api**

- `client_id`: ID khách hàng của dự án Google API.
- `client_secrets`: Mật khẩu bí mật của dự án Google API.
- `redirect_url`: URL chuyển hướng sau khi người dùng hoàn thành quy trình xác nhận Google.
- `youtube_redirect_url`: URL chuyển hướng sau khi người dùng thêm hồ sơ Youtube.
- `google_profile_add_redirect_url`: URL chuyển hướng sau khi người dùng thêm hồ sơ Google.
- `api_key`: Chìa khóa API từ Google API.
- `dynamic_link`: Đường dẫn động của Firebase (sử dụng cho chức năng chia sẻ ứng dụng động).
- `youtube_webhook_url`: URL webhook để nhận các sự kiện thời gian thực từ YouTube.

**twitter_api**

- `api_key`: Chìa khóa API từ Twitter.
- `secret_key`: Mật khẩu bí mật từ Twitter.
- `login_redirect_url`: URL chuyển hướng sau khi người dùng hoàn thành quy trình xác nhận Twitter.
- `redirect_url`: URL chuyển hướng sau khi người dùng thêm hồ sơ Twitter.
- `app_name`: Tên ứng dụng Twitter được đăng ký.
- `webhook_url`: URL webhook để nhận các sự kiện thời gian thực từ Twitter.
- `webhook_environment`: Môi trường webhook Twitter (development hoặc production).
- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Twitter.

**linkedIn_api**

- `client_id`: ID khách hàng của tài khoản LinkedIn.
- `client_secret`: Mật khẩu bí mật của tài khoản LinkedIn.
- `redirect_url`: URL chuyển hướng sau khi người dùng hoàn thành quy trình xác thực LinkedIn.
- `app_name`: Tên ứng dụng LinkedIn được đăng ký.
- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ LinkedIn.

**instagram_api**

- `client_id`: ID ứng dụng Instagram.
- `client_secret`: Bí mật ứng dụng Instagram.
- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Instagram.

**instagram_business_api**

- `client_id`: ID ứng dụng Instagram Business.
- `client_secret`: Mật khẩu của ứng dụng Instagram Business.
- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Instagram Business.

**pinterest**

- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Pinterest.

**tumblr_api**

- `update_time_frequency_value`,`update_time_frequency_factor`: Tần suất cập nhật dữ liệu từ Tumblr.

Tất cả thông tin cần thiết để cấu hình tệp này sẽ phụ thuộc vào cài đặt cụ thể của bạn và các dịch vụ bạn chọn sử dụng. Đảm bảo kiểm tra tất cả các chi tiết cho thực hiện đúng.
