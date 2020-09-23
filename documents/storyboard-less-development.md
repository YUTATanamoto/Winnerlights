# iOS Development without StoryBoard  
## Setup  
- TARGETS > Info内にある'Main storyboard file base name'を削除  
- TARGETS > Info > Application Scene Manifest > Scene Configuration > Application Session Role > Item0(Default Configura... 内にある'Storyboard Name'を削除  
- AppDelegate.swiftで初回の起動画面を設定  
  AppDelegate.swift
  ```
  class AppDelegate: UIResponder, UIApplicationDelegate {

      var window: UIWindow?

      func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
          // Override point for customization after application launch.

          window = UIWindow(frame: UIScreen.main.bounds)
          window?.rootViewController = ViewController()
          window?.makeKeyAndVisible()

          return true
      }
  }
  ```  
- SceneDelegate.swiftで初回の起動画面を設定  
  SceneDelegate.swif
  ```
  class SceneDelegate: UIResponder, UIWindowSceneDelegate {

      var window: UIWindow?

      func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
          // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
          // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
          // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
          guard let scene = (scene as? UIWindowScene) else { return }
          window = UIWindow(windowScene: scene)
          window?.rootViewController = ViewController()
          window?.makeKeyAndVisible()
      }
  }
  ```  
- iOS13以前のバージョンに対応  
    AppDelegate.swift
  ```
  @UIApplicationMain
  class AppDelegate: UIResponder, UIApplicationDelegate {

      var window: UIWindow?

      func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
          // Override point for customization after application launch.

          if #available(iOS 13.0, *) {

          } else {
              //iOS13以前のときだけ呼ばれる
              window = UIWindow(frame: UIScreen.main.bounds)
              window?.rootViewController = ViewController()
              window?.makeKeyAndVisible()
          }

          return true
      }

      // MARK: UISceneSession Lifecycle

      @available(iOS 13.0, *)
      func application(_ application: UIApplication, configurationForConnecting connectingSceneSession: UISceneSession, options: UIScene.ConnectionOptions) -> UISceneConfiguration {
          // Called when a new scene session is being created.
          // Use this method to select a configuration to create the new scene with.
          return UISceneConfiguration(name: "Default Configuration", sessionRole: connectingSceneSession.role)
      }

      @available(iOS 13.0, *)
      func application(_ application: UIApplication, didDiscardSceneSessions sceneSessions: Set<UISceneSession>) {
          // Called when the user discards a scene session.
          // If any sessions were discarded while the application was not running, this will be called shortly after application:didFinishLaunchingWithOptions.
          // Use this method to release any resources that were specific to the discarded scenes, as they will not return.
      }


  }
  ```  

  SceneDelegate.swift
  ```
  @available(iOS 13.0, *)
  class SceneDelegate: UIResponder, UIWindowSceneDelegate {

      var window: UIWindow?

      func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
          guard let scene = (scene as? UIWindowScene) else { return }
          window = UIWindow(windowScene: scene)
          window?.rootViewController = ViewController()
          window?.makeKeyAndVisible()
      }
      func sceneDidDisconnect(_ scene: UIScene) {...}

      func sceneDidBecomeActive(_ scene: UIScene) {...}

      func sceneWillResignActive(_ scene: UIScene) {...}

      func sceneWillEnterForeground(_ scene: UIScene) {...}

      func sceneDidEnterBackground(_ scene: UIScene) {...}

  }
  ```
