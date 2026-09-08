Spring Security

Spring Security Filter Chain

⚙️ Filter Chain & Core
doFilter() (method of Filter, not doFilterChain)
FilterChain (Servlet API interface)
FilterChainProxy ✅
DelegatingFilterProxy ✅
OncePerRequestFilter ✅


🔐 Authentication Components
AuthenticationManager ✅
AuthenticationProvider ✅
👉 ✅ UsernamePasswordAuthenticationFilter

👤 User Details Layer
👉 ✅ UserDetailsService
👉 ✅ UserDetails
GrantedAuthority ✅
	
⚠️ Exception Handling
👉 ✅ ExceptionTranslationFilter

🔑 Security Utilities
PasswordEncoder ✅
SecurityContextHolder ✅


RBAC 

PreAuthorize
hasRole()
hasAuthority()
How to Enable It ?

JWT
Statefull or Stateless
Where it is Stored ?
How to Encode or Decode?
Flow 
Encode/Decode


CSRF vs CQRS

What else topic i need to study from Spring Security ?