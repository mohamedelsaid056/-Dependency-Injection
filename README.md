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
