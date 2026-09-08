

🚀 From “Almost a Minute” to “Just a Few Seconds”: Spring Boot Startup Hack  
  
Frustration:  
Restart app → wait… wait… wait.  
  
By the day's evening, I’d wasted hours just watching Spring Boot start. 😩  
  
❌ Problems I found:  
• Scanning every package on the classpath  
• Eagerly creating all beans (even unused ones)  
• DB connections opening at startup  
• Auto-configurations for features we didn’t need  
  
  
✅ Fixes that worked:  
  
1. Lazy Init:  
  
spring.main.lazy-initialization=true  
  
👉 Beans load only when first used, not all at startup.  
⏱ Cut startup by ~40-50%  
  
  
  
2. Smart Scanning  
  
@SpringBootApplication(scanBasePackages="com.myapp.core")  
  
👉 Spring scans only your core packages, not everything.  
⏱ Cut more seconds off  
  
  
  
3. Conditional Config  
  
@ConditionalOnProperty(name="feature.enabled", havingValue="true")  
  
👉 Optional features load only if enabled.  
⏱ More seconds saved  
  
  
🎬 Netflix Analogy for Lazy vs Eager Init:  
Netflix doesn’t download all episodes of a show before you watch. It streams episode 1 immediately, and the rest only if you keep watching.  
  
(Imagine Netflix loading every movie and series thumbnail, trailer, and subtitles in all languages before letting you watch anything. Startup takes forever, even though you’ll probably just watch one show. Shown in an image for example.)  
  
  
📊 Before vs After:  
BEFORE: [████████████████████████] ~40s-45s 😴  
AFTER:  [███] ~ 5s-8s ⚡  
  
⚡ Quick wins for you:  
👉 Enable lazy init  
👉 Audit @ComponentScan  
👉 Review auto-configs  
👉 Profile startup with Actuator