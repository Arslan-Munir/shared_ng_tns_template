Using NS Version 6.7.8, you may face problems in running application. To solve these,

1. In package.json remove @angular/http, since it is no longer available.
2. In dev depedencies, change version of @angular/semnatic from 2.0.0 to 9.0.0

3. Run npm i

4. Change in webpack.config.js. 
  Find CopyWebpackPlugin settings.
  Replace exsisting fonts and .jpg, .png settings with 
    new CopyWebpackPlugin({
              patterns: [
                { from: 'assets/**', noErrorOnMissing: true, globOptions: { dot: false, ...copyIgnore } },
                { from: 'fonts/**', noErrorOnMissing: true, globOptions: { dot: false, ...copyIgnore } },
                { from: '**/*.jpg', noErrorOnMissing: true, globOptions: { dot: false, ...copyIgnore } },
                { from: '**/*.png', noErrorOnMissing: true, globOptions: { dot: false, ...copyIgnore } },
              ],
            }),
            
5. Place these lines at above entryModule declaration. Remove appResourcesFullPath if twice.
  const appResourcesFullPath = resolve(projectRoot, appResourcesPath);
  const copyIgnore = { ignore: [`${relative(appPath, appResourcesFullPath)}/**`] };

6. In tsconfig.tns.json, add a new section to disable Ivy
  "angularCompilerOptions": {
    "enableIvy": false
  }

7. Run ng serve for web and tns run android --env.aot for mobile
