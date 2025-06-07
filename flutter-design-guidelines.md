# Flutter App 项目开发指南

本文档定义了 Flutter 应用开发的规范和最佳实践，确保代码质量、性能和可维护性。

## 技术栈规范

- 目标平台：iOS/Android
- Flutter SDK 版本：3.22.0
- Dart SDK 版本：3.4.0
- 状态管理： ChangeNotifier, Provider
- 网络请求： Dio
- 国际化： intl
- 日志： talker
- 路由： go_router
- 依赖注入： get_it
- 路由管理： go_router
- 日志： talker
- 资源管理： flutter_gen
- 代码生成： build_runner, freezed, json_serializable
- 代码风格： lints
- 代码覆盖率： coverage
- 代码质量： dart_code_metrics
- 代码分析： dart_analyzer
- 代码格式化： dart_format
- 代码覆盖率： coverage
- 代码质量： dart_code_metrics

## 目录结构

对于已有项目的目录结构，我们可以采用以下策略：

1. 保持原有目录结构：如果项目已经有了清晰的目录结构，可以保持不变。
2. 简化目录结构：如果项目的目录结构过于复杂，可以考虑简化。
3. 引入新的目录结构：如果项目的目录结构需要进行调整，可以引入新的目录结构。

对于新项目，我们可以采用以下策略：

1. 对于小型项目 ：可以只使用简单的功能结构，快速开发
2. 对于中型项目 ：可以选择性地采用完整的分层架构
3. 对于大型项目 ：可以充分利用所有的架构层次，确保可维护性和可扩展性

目录结构的核心哲学是**简单的事情简单做，复杂的事情有章法**。

下面是一个新项目目录结构示例：

```bash
lib/
├── main.dart                   # 应用入口文件
├── app/
│   ├── app.dart                # 应用主类，配置MaterialApp
│   ├── routes.dart             # 路由配置
│   └── config/                 # 应用配置
│       ├── app_config.dart     # 应用基础配置（API地址、版本等）
│       └── environment.dart    # 环境配置（开发、测试、生产）
├── core/                       # 核心基础设施层
│   ├── constants/              # 常量定义
│   │   ├── app_constants.dart  # 应用常量（尺寸、时间等）
│   │   ├── api_constants.dart  # API相关常量
│   │   └── string_constants.dart # 字符串常量
│   ├── errors/                 # 错误处理
│   │   ├── exceptions.dart     # 自定义异常类
│   │   ├── failures.dart       # 失败类型定义
│   │   └── error_handler.dart  # 全局错误处理器
│   ├── utils/                  # 工具类
│   │   ├── date_utils.dart     # 日期工具
│   │   ├── validation_utils.dart # 验证工具
│   │   ├── format_utils.dart   # 格式化工具
│   │   └── logger.dart         # 简化的日志工具类
│   ├── extensions/             # Dart扩展
│   │   ├── string_extension.dart # 字符串扩展
│   │   ├── datetime_extension.dart # 日期扩展
│   │   └── context_extension.dart # BuildContext扩展
│   ├── network/                # 网络层
│   │   ├── api_client.dart     # HTTP客户端封装
│   │   ├── network_info.dart   # 网络状态检测
│   │   └── interceptors/       # 网络拦截器
│   │       ├── auth_interceptor.dart # 认证拦截器
│   │       ├── logging_interceptor.dart # 日志拦截器
│   │       └── error_interceptor.dart # 错误拦截器
│   ├── services/               # 核心基础服务
│   │   ├── log_service.dart    # 日志服务（支持多输出）
│   │   ├── storage_service.dart # 本地存储服务
│   │   ├── cache_service.dart  # 缓存服务
│   │   └── device_service.dart # 设备信息服务
│   └── di/                     # 依赖注入
│       ├── injection.dart      # 依赖注入配置
│       └── service_locator.dart # 服务定位器
├── features/                   # 功能模块
│   ├── auth/                   # 认证功能（复杂功能示例）
│   │   ├── data/
│   │   │   ├── datasources/
│   │   │   │   ├── auth_local_datasource.dart # 本地数据源
│   │   │   │   └── auth_remote_datasource.dart # 远程数据源
│   │   │   ├── models/
│   │   │   │   ├── user_model.dart # 用户数据模型
│   │   │   │   └── auth_response_model.dart # 认证响应模型
│   │   │   └── repositories/
│   │   │       └── auth_repository_impl.dart # 认证仓库实现
│   │   ├── domain/             # 业务逻辑层
│   │   │   ├── entities/
│   │   │   │   └── user.dart   # 用户实体
│   │   │   ├── repositories/
│   │   │   │   └── auth_repository.dart # 认证仓库接口
│   │   │   └── usecases/
│   │   │       ├── login_usecase.dart # 登录用例
│   │   │       └── logout_usecase.dart # 登出用例
│   │   ├── presentation/
│   │   │   ├── pages/
│   │   │   │   ├── login_page.dart # 登录页面
│   │   │   │   └── register_page.dart # 注册页面
│   │   │   ├── widgets/
│   │   │   │   ├── login_form.dart # 登录表单组件
│   │   │   │   └── auth_button.dart # 认证按钮组件
│   │   │   └── providers/
│   │   │       └── auth_provider.dart # 认证状态管理
│   ├── profile/                # 用户资料（简单功能示例）
│   │   ├── profile_repository.dart # 用户资料仓库
│   │   ├── profile_page.dart   # 用户资料页面
│   │   └── profile_provider.dart # 用户资料状态管理
│   └── settings/               # 设置功能
│       ├── settings_repository.dart # 设置仓库
│       └── settings_page.dart  # 设置页面
├── shared/                     # 共享资源
│   ├── widgets/                # 共享UI组件
│   │   ├── common/
│   │   │   ├── custom_button.dart # 自定义按钮
│   │   │   ├── custom_text_field.dart # 自定义输入框
│   │   │   ├── loading_widget.dart # 加载组件
│   │   │   └── error_widget.dart # 错误显示组件
│   │   ├── dialogs/
│   │   │   ├── confirm_dialog.dart # 确认对话框
│   │   │   └── info_dialog.dart # 信息对话框
│   │   └── layouts/
│   │       ├── app_scaffold.dart # 应用脚手架
│   │       └── responsive_layout.dart # 响应式布局
│   ├── services/               # 共享业务服务
│   │   ├── api_service.dart    # API服务封装
│   │   ├── auth_service.dart   # 认证服务
│   │   ├── notification_service.dart # 通知服务
│   │   └── analytics_service.dart # 分析服务
│   ├── themes/                 # 主题配置
│   │   ├── app_theme.dart      # 应用主题
│   │   ├── app_colors.dart     # 颜色定义
│   │   ├── app_text_styles.dart # 文本样式
│   │   └── app_dimensions.dart # 尺寸定义
│   └── models/                 # 共享数据模型
│       ├── base_model.dart     # 基础模型类
│       ├── api_response.dart   # API响应模型
│       └── pagination_model.dart # 分页模型
├── l10n/                       # 国际化
│   ├── app_en.arb             # 英文翻译
│   ├── app_zh.arb             # 中文翻译
│   └── l10n.dart              # 国际化配置
├── gen/                        # 自动生成文件
│   ├── assets.gen.dart        # 资源文件生成
│   ├── colors.gen.dart        # 颜色生成
│   └── fonts.gen.dart         # 字体生成
└── test/                       # 测试文件
    ├── unit/                   # 单元测试
    │   ├── core/
    │   ├── features/
    │   └── shared/
    ├── widget/                 # Widget测试
    │   ├── pages/
    │   └── widgets/
    ├── integration/            # 集成测试
    ├── mocks/                  # 模拟对象
    │   ├── mock_services.dart
    │   └── mock_repositories.dart
    └── helpers/                # 测试辅助工具
        ├── test_helpers.dart
        └── pump_app.dart
```

## 注释规范

- **类注释**

  - 描述类的用途和功能
  - 说明主要的使用场景
  - 提供使用示例

- **方法注释**
  - 描述方法的功能
  - 说明参数的含义和约束
  - 描述返回值
  - 列出可能抛出的异常

注释示例：

````dart
/// 用户认证服务
///
/// 提供用户登录、注册、登出等功能。
/// 支持多种认证方式：邮箱密码、手机号验证码、第三方登录。
///
/// 使用示例：
/// ```dart
/// final authService = AuthService();
/// final user = await authService.login('email@example.com', 'password');
/// ```
class AuthService {
  bool _isLoggedIn = false;

  /// 当前用户是否已登录
  bool get isLoggedIn => _isLoggedIn;

  /// 用户登录
  ///
  /// 使用邮箱和密码进行用户认证。
  ///
  /// * [email] 用户邮箱地址，必须是有效的邮箱格式
  /// * [password] 用户密码，长度至少6位
  ///
  /// 返回登录成功的用户信息。
  ///
  /// 抛出 [AuthException] 当认证失败时
  /// 抛出 [NetworkException] 当网络请求失败时
  Future<User> login(String email, String password) async {
    // 实现登录逻辑
  }
}
````

## 测试规范

### 测试类型

- **单元测试**: 测试单个函数或类，使用 `test` 或 `mocktail` 库
- **Widget 测试**: 测试 UI 组件，使用 `flutter_test` 库
- **集成测试**: 测试完整的用户流程，使用 `flutter_driver` 库

### `mocktail`测试框架

推荐采用`MockTail`库进行测试，它提供了一种简单的方式来模拟和验证对象的行为，并且可以轻松地生成测试覆盖率报告。
MockTail 是一个用于 Dart 和 Flutter 应用程序的模拟库，它提供了一种简单的方式来模拟和验证对象的行为。MockTail 可以轻松地生成测试覆盖率报告，并且可以轻松地集成到 CI/CD 管道中。

MockTail 提供了以下功能：

- 模拟对象：MockTail 可以轻松地模拟对象的行为，包括方法调用、属性访问和异常抛出。
- 验证：MockTail 可以轻松地验证对象的行为，包括方法调用、属性访问和异常抛出。
- 生成测试覆盖率报告：MockTail 可以轻松地生成测试覆盖率报告，包括方法调用、属性访问和异常抛出。

使用示例：

```dart
import 'package:mocktail/mocktail.dart';
import 'package:test/test.dart';

class Food {}
class Chicken extends Food {}
class Tuna extends Food {}

// A Real Cat class
class Cat {
  String sound() => 'meow!';
  bool likes(String food, {bool isHungry = false}) => false;
  void eat<T extends Food>(T food) {}
  final int lives = 9;
}

// A Mock Cat class
class MockCat extends Mock implements Cat {}

void main() {
  group('Cat', () {
    setUpAll(() {
      // Register fallback values when using
      // `any` or `captureAny` with custom objects.
      registerFallbackValue(Chicken());
      registerFallbackValue(Tuna());
    });

    late Cat cat;

    setUp(() {
      cat = MockCat();
    });

    test('example', () {
      // Stub a method before interacting with the mock.
      when(() => cat.sound()).thenReturn('purr');

      // Interact with the mock.
      expect(cat.sound(), 'purr');

      // Verify the interaction.
      verify(() => cat.sound()).called(1);

      // Stub a method with parameters
      when(
        () => cat.likes('fish', isHungry: any(named: 'isHungry')),
      ).thenReturn(true);
      expect(cat.likes('fish', isHungry: true), isTrue);

      // Verify the interaction.
      verify(() => cat.likes('fish', isHungry: true)).called(1);

      // Interact with the mock.
      cat
        ..eat(Chicken())
        ..eat(Tuna());

      // Verify the interaction with specific type arguments.
      verify(() => cat.eat<Chicken>(any())).called(1);
      verify(() => cat.eat<Tuna>(any())).called(1);
      verifyNever(() => cat.eat<Food>(any()));
    });
  });
}
```

### 测试覆盖率

- 目标测试覆盖率: 80% 以上
- 关键业务逻辑: 100% 覆盖
- 使用 `flutter test --coverage` 生成覆盖率报告

## 依赖包管理

### 包选择原则

- **官方优先**: 优先选择 Flutter 团队维护的包
- **活跃度**: 选择活跃维护的包
- **稳定性**: 避免使用 alpha 或 beta 版本的包
- **大小**: 考虑包的大小对应用体积的影响，避免只需要一小部分实现而引入繁重的依赖
- **文档**: 选择文档齐全的包

### pubspec.yaml 管理

核心管理原则：

1. **分类组织** - 按功能模块分组依赖
2. **版本控制** - 合理使用版本约束策略
3. **注释说明** - 为每个分组添加清晰注释
4. **定期维护** - 及时清理和更新依赖

完整示例：

```yaml
name: flutter_enterprise_app
description: 企业级Flutter应用模板
version: 1.2.0+12

# 环境约束
environment:
  sdk: '>=3.0.0 <4.0.0'
  flutter: '>=3.16.0'

dependencies:
  flutter:
    sdk: flutter

  # 核心状态管理 (锁定版本确保稳定性)
  bloc: 8.1.2
  flutter_bloc: 8.1.3
  equatable: 2.0.5

  # 网络层
  dio: ^5.3.2                    # HTTP客户端
  retrofit: ^4.0.3               # API代码生成
  json_annotation: ^4.8.1       # JSON序列化注解
  connectivity_plus: ^5.0.1      # 网络状态检测

  # 数据持久化
  shared_preferences: ^2.2.2     # 键值存储
  sqflite: ^2.3.0               # SQLite数据库
  hive: ^2.2.3                  # NoSQL数据库
  hive_flutter: ^1.1.0

  # UI组件库
  cupertino_icons: ^1.0.6       # iOS风格图标
  flutter_svg: ^2.0.7           # SVG图片支持
  cached_network_image: ^3.3.0  # 网络图片缓存
  shimmer: ^3.0.0               # 骨架屏效果
  pull_to_refresh: ^2.0.0       # 下拉刷新

  # 工具类
  intl: ^0.18.1                 # 国际化
  path_provider: ^2.1.1         # 文件路径
  url_launcher: ^6.2.1          # 外部链接
  package_info_plus: ^4.2.0     # 应用信息
  device_info_plus: ^9.1.0      # 设备信息

  # 平台特性
  permission_handler: ^11.0.1    # 权限管理
  image_picker: ^1.0.4          # 图片选择
  camera: ^0.10.5+5             # 相机功能
  geolocator: ^10.1.0           # 地理位置

  # 安全相关
  crypto: ^3.0.3                # 加密算法
  local_auth: ^2.1.6           # 生物识别

  # 分析统计
  firebase_analytics: ^10.7.0   # Firebase分析
  firebase_crashlytics: ^3.4.8 # 崩溃统计

dev_dependencies:
  flutter_test:
    sdk: flutter

  # 代码质量
  flutter_lints: ^3.0.1         # 官方代码规范
  dart_code_metrics: ^5.7.6     # 代码度量
  import_sorter: ^4.6.0         # 导入排序

  # 测试框架
  mocktail: ^1.0.0              # Mock测试
  bloc_test: ^9.1.4             # Bloc测试
  integration_test:              # 集成测试
    sdk: flutter
  patrol: ^2.6.0                # UI测试增强

  # 构建工具
  build_runner: ^2.4.7          # 代码生成
  json_serializable: ^6.7.1     # JSON序列化生成
  retrofit_generator: ^7.0.8    # API代码生成
  hive_generator: ^2.0.1        # Hive代码生成

  # 部署工具
  flutter_launcher_icons: ^0.13.1  # 应用图标生成
  flutter_native_splash: ^2.3.5    # 启动屏生成

# Flutter配置
flutter:
  uses-material-design: true

  # 资源文件 (按类型分组)
  assets:
    # 图片资源
    - assets/images/common/
    - assets/images/icons/
    - assets/images/backgrounds/
    - assets/images/avatars/

    # 配置文件
    - assets/config/
    - assets/data/

    # 国际化文件
    - assets/i18n/

    # 动画文件
    - assets/animations/

  # 字体配置
  fonts:
    # 主要字体族
    - family: AppFont
      fonts:
        - asset: assets/fonts/app/AppFont-Light.ttf
          weight: 300
        - asset: assets/fonts/app/AppFont-Regular.ttf
          weight: 400
        - asset: assets/fonts/app/AppFont-Medium.ttf
          weight: 500
        - asset: assets/fonts/app/AppFont-Bold.ttf
          weight: 700

    # 图标字体
    - family: CustomIcons
      fonts:
        - asset: assets/fonts/icons/CustomIcons.ttf

# 依赖覆盖 (谨慎使用)
dependency_overrides:
  # 仅在解决版本冲突时使用
  # analyzer: ^5.13.0  # 解决某些包的分析器版本冲突

# Flutter配置
flutter_launcher_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/images/app_icon.png"
  adaptive_icon_background: "#FFFFFF"
  adaptive_icon_foreground: "assets/images/app_icon_foreground.png"

flutter_native_splash:
  color: "#FFFFFF"
  image: "assets/images/splash_logo.png"
  android_12:
    image: "assets/images/splash_logo_android12.png"
    color: "#FFFFFF"
```
