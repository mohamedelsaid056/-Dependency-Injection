# الDependency-Injection 
- في مشكله هاتقابلني وانا شغال في عموما في اي appliction وهي ان عندي components مخنلفه انا شغال فيها مع team كل developer شغال علي حاجه معينه 
- مثال في mvc ناس شغاله علي view فثط ونفس القصه علي controller و models 
فبالتالي بتظهر مشاكل ان كل developer يعمل test للكود بتاعه وبالتالي انا محتاج افصل كل components عند بعضها بحيث انها لا تعتمد علي الاخر عشان  اعمل
ال test for each component lonely without dependency  
 

بدايه فصل ال components اننا نبدا بفصل اي business logic بكتبه داخل ال controller علشان موضوع testing وان ممكن كل component يكون شغال عليه developer مختلف وبالتالي احتاجنا يكون في هناك layer نلم فيها كل business calculations, business validations  ونسميها 𝐒𝐞𝐫𝐯𝐢𝐜𝐞

## مما سبق نستنتج 
ان ممنوع نكتب اي  business logic لان د هايصعب عمليه testing 
## ايه هي 𝐒𝐞𝐫𝐯𝐢𝐜𝐞 
- عباره عن middle layer ما بين presentation layer(view) وما بين data layer 
- كده اقدر من خلالها اعمل test علي business logic لاني فصلته في layer لوحده بعيدا عن controller
- في controller هاعمل invoke ل 𝐒𝐞𝐫𝐯𝐢𝐜𝐞 بحيث استخدم الي فيها من business logic واقدر كمان استدعي ال data من provider

  
  
<div align="center">
<img src="https://github.com/mohamedelsaid056/-Dependency-Injection/assets/138726588/ed19dfea-13b1-4bf2-996e-b019fe4837c8" alt="" width="700" />
  
</div>

- بنفذ ال 𝐒𝐞𝐫𝐯𝐢𝐜𝐞 في الغالب في project منفصل عن ال project الي فيه mvc وبنستدعيه
```
  // service

   public class UserService
 {
     public IEnumerable<User> GetUsers()
     {
         // implementation for business calculations, business validations
     }
 }

   // invoke service in controller 

 public class UserController : Controller
 {
     // creating object from service 
     UserService userService = new UserService();
     public ActionResult Index()
     {
         var users = userService.GetUsers();
         return View(users);
     }
 }
   
 ```


## مشكله اخري تعرف ب Direct Dependency 

انا عملت invoke for service في controller و ظهرت لي مشكله ان انا Developer1 شغال علي controller و Developer2 شغال علي service انا عملت object from service منين هاعرف ال method الي جوه ال service لو لسه ال service مخلتصتش وبالتالي
### الحل 
انا محتاج Developer1 شغال علي controller اعمل Abstraction لل method الي عاوزها جوه interface واقول ل Developer2  يا ريت لو implement this interface 


والتالي نعدل الكود علي كده 
<div>
   <div  align="center" >
   <img src="https://github.com/mohamedelsaid056/-Dependency-Injection/assets/138726588/9322221d-00f8-4623-80fe-db2be3d4f4c2" alt="" width="600" />
   </div>

   <div align="center">
   <img src="https://github.com/mohamedelsaid056/-Dependency-Injection/assets/138726588/04e2c2a4-8871-4e23-8ee7-b6abbd6109b6" alt="" width="600" /> 
   </div>
  
 
</div>

##  مشكله اخري تعرف ب 𝐭𝐢𝐠𝐡𝐭𝐲 𝐜𝐨𝐮𝐩𝐥𝐞
 - الكود الي فوق ظهرت لي مشكله ان انا Developer1 شغال علي controller و Developer2 شغال علي service انا محتاج علشان اشتغل علي ال controller واعمل ال test عليه محتاج Developer2 يكون مخلص شغله في service لاني عملت Create object for service using 𝐧𝐞𝐰 key word وفي شغل ال team دي حاجه مش مظبوطه وبالتالي واجهتني المشكله المشهوره 𝐭𝐢𝐠𝐡𝐭𝐲 𝐜𝐨𝐮𝐩𝐥𝐞 
- كمان لو حصل تيغرات في Service هاتسمع عند controller
-  في testing دايما هاتكون عندي مشكله 
 

### الحل Dependency Inversion Principle (DIP) 
- وعلشان احل الاشكاليه دي انا محتاج يحصل creation ل service class من غير ما استخدم كلمه new محتاج وسط "container"  هو الي يقوم بالمهمه دي 


