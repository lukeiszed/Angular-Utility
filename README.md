# ANGULAR UTILS
Chars:  `   ~

## Install SCSS:
	When creating new project: 		ng new My_New_Project --style=sass    
									npm install node-sass --save-dev
									
	On existing project: 			ng set defaults.styleExt scss		  
									npm install node-sass --save-dev   
									change .angular-cli.json -> "styles": ["styles.scss"]
									
									
## Install BOOTSTRAP:
	On existing project:			npm install ngx-bootstrap bootstrap@next jquery tether popper.js --save
	
	Add to style.scss:			    @import "../node_modules/bootstrap/scss/bootstrap";
	
	Add to angular-cli.json:		In "scripts" section:
									"../node_modules/jquery/dist/jquery.js",
									"../node_modules/popper.js/dist/umd/popper.min.js",
									"../node_modules/tether/dist/js/tether.js",
									"../node_modules/bootstrap/dist/js/bootstrap.js"
									
									
## Load Settings from file:
	In app.modules.ts: 				Add this code before the @NgModule({}) declaration:
									export function InitConfig(settings: SettingsService) { return () => settings.LoadConf();}
									
									Add in the provider array this code:
									 {provide: APP_INITIALIZER, useFactory: InitConfig , deps: [SettingsService], multi: true}
									
	In settings.service.ts			Add method:
									 LoadConf() {
										return new Promise((resolve, reject) => {
											this.http.get<any>('assets/config/config.json').subscribe((conf: any) => {
											this.settings = conf;
											resolve();
										}, error => reject());
										});
									}
									

									
