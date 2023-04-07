# Sử dụng ReactJS với create-react-app hoặc webpack

```jsx
npx create-react-app my-app
npm status
```

Webpack là một công cụ mạnh mẽ để đóng gói các tệp JavaScript và các tài nguyên khác như CSS, hình ảnh và font chữ thành các gói tải về và triển khai. Nó cũng cung cấp các tính năng tối ưu hóa và nén mã JavaScript để giảm thời gian tải và tăng hiệu suất của ứng dụng. Để sử dụng Webpack trong ứng dụng React, bạn có thể sử dụng các công cụ như **`create-react-app`**
 hoặc cấu hình webpack của riêng bạn. Nếu bạn muốn tìm hiểu thêm về cách cấu hình webpack cho ứng dụng React của mình, bạn có thể tham khảo trang web chính thức của webpack hoặc các tài liệu tham khảo khác trên mạng.

## webpack

Webpack là một công cụ đóng gói (bundling tool) mã nguồn JavaScript cho phép bạn tạo ra các file bundle hoặc các tệp đóng gói được tải về từ máy chủ. Nó cho phép bạn quản lý các phụ thuộc và tệp của ứng dụng và cho phép tạo ra các tệp được tối ưu hóa để cải thiện hiệu suất và tải trang.

Cấu hình webpack là một quá trình khá phức tạp, nhưng nó cho phép bạn tùy chỉnh các phần của quá trình đóng gói và cài đặt các plugin để tối ưu hóa hiệu suất của ứng dụng của bạn. Để cấu hình webpack để sử dụng trong ứng dụng React của bạn, bạn có thể làm theo các bước sau:

1. Tạo tệp package.json bằng lệnh **`npm init`** và cài đặt webpack và webpack-cli bằng lệnh sau:

```jsx
npm install webpack webpack-cli --save-dev
```

1.  Tạo một tệp cấu hình webpack bằng cách tạo tệp **`webpack.config.js`** và cấu hình các module và plugin của bạn như sau:

```jsx
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = {
  entry: './src/index.js', // tao thu muc src/index.js
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',// install và khai bao .babelrc thành công 
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
        template: './public/index.html', // tạo thu muc public/ index.html 
        filename: 'index.html',
    }),
  ],
};
// public/ index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
// tao thu muc src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

function App() {
  return (
    <div>
      <h1>Hello, world!</h1>
      <p>Tôi tên là Nguễn Thị Kim Lam </p>
      <p>Sinh năm 1999</p>
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

1. Cài đặt babel-loader để biên dịch các tệp JavaScript mới hơn bằng lệnh sau:

```jsx
npm install babel-loader @babel/core @babel/preset-env @babel/preset-react --save-dev
```

1. Cài đặt style-loader và css-loader để xử lý các tệp CSS trong ứng dụng của bạn:

```jsx
npm install style-loader css-loader --save-dev
```

1. Tạo một tệp index.html trong thư mục public để webpack có thể sử dụng nó và cài đặt React và ReactDOM bằng lệnh sau:

```jsx
npm install react react-dom --save
```

1. Cấu hình npm script để chạy webpack:

```jsx
// sau khi install cac lib tren
{
  "devDependencies": {
    "@babel/core": "^7.21.4",
    "@babel/preset-env": "^7.21.4",
    "@babel/preset-react": "^7.18.6",
    "babel-loader": "^9.1.2",
    "clean-webpack-plugin": "^4.0.0",
    "css-loader": "^6.7.3",
    "html-webpack-plugin": "^5.5.0",
    "style-loader": "^3.3.2",
    "webpack": "^5.78.0",
    "webpack-cli": "^5.0.1",
    "webpack-dev-server": "^4.13.2"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "scripts": {
    "start": "webpack-dev-server --mode development --open",
    "build": "webpack --mode production"
  }
}
```

1. Cài đặt các plugin cần thiết

```jsx
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
// tạo .babelrc
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

8 . Chạy ứng dụng của bạn với lệnh **`npm start`**
 hoặc tạo một file build với lệnh **`npm run build`**