SpringBoot Notes

### 常用注解

1. **@SpringBootApplication**：
   - 这是 Spring Boot 应用程序的核心注解，它是一个方便的注解，包含了 `@Configuration`、`@EnableAutoConfiguration` 和 `@ComponentScan`。
   - 它通常用于主应用类上。
2. **@Configuration**：
   - 表示该类包含一些方法，这些方法会返回一个对象，该对象应该被注册为 Spring 上下文中的 bean。
   - 通常与 `@Bean` 注解一起使用。
3. **@Bean**：
   - 用在方法上，表示将该方法的返回值添加到 Spring 容器中，作为一个 Bean。
4. **@Component**：
   - 用于类级别，表示将该类注册为 Spring 容器中的一个 Bean。
5. **@Repository**、**@Service**、**@Controller**、**@RestController**：
   - 这些注解是 `@Component` 的特化，用于对应用程序的不同层进行分层和分类。
   - `@Repository` 用于持久层，`@Service` 用于服务层，`@Controller` 用于表现层（Spring MVC），而 `@RestController` 是 `@Controller` 和 `@ResponseBody` 的组合，用于创建 RESTful 服务。
6. **@Autowired**：
   - 用于自动注入依赖。可以用在构造函数、字段和方法上。
7. **@RequestMapping**、**@GetMapping**、**@PostMapping**、**@PutMapping**、**@DeleteMapping**：
   - 这些注解用于处理 HTTP 请求。`@RequestMapping` 是一个通用注解，可以处理任何类型的请求，而其它注解是特定于 HTTP 方法的。
8. **@PathVariable**、**@RequestParam**、**@RequestBody**：
   - 用于处理控制器方法的参数。`@PathVariable` 用于从 URL 中获取参数，`@RequestParam` 用于从请求参数中获取参数，`@RequestBody` 用于获取 HTTP 请求体中的数据。
9. **@Value**：
   - 用于将配置文件中的值注入到字段中。
10. **@Profile**：
    - 用于指定某些 Bean 只有在特定的环境配置下才会被创建。
11. **@EnableJpaRepositories**、**@EntityScan**、**@EnableTransactionManagement**：
    - 这些注解与 JPA 和数据库交互相关。
12. **@Scheduled**：
    - 用于创建计划任务。
13. **@EnableCaching**、**@Cacheable**、**@CacheEvict**、**@CachePut**：
    - 这些注解与缓存相关。