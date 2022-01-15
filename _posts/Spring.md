@ModelAttribute 와 커맨드 객체(Command Object)   
[참조]<https://medium.com/webeveloper/modelattribute-%EC%99%80-%EC%BB%A4%EB%A7%A8%EB%93%9C-%EA%B0%9D%EC%B2%B4-command-object-42c14f268324>   

# validation 관련 처리

[사용]   
@RequestMapping("/create")
public String insert2(@ModelAttribute("dto") ContentDto contentDto, BindingResult result)   
{   
  String page = "createDonePage";
  
  ContentValidator validator = new ContentValidator();   
  validator.validate(contentDto, result);   
  if (result.hasErrors())   
    page = "createPage";   
    
  return page;   
}


[처리]   
public class ContentValidator implements Validator {   

@Override
public boolean supports(Class<?> arg0) {   
  return ContentDto.class.isAssignableForm(arg0);   
}   

@Override   
public void validate(Object obj, Errors errors) {   
  ContentDto dto = (ContentDto)obj;   

  String sWriter = dto.getWriter();
  if (sWriter == null || sWriter.trim().isEmpty()) {
    System.out.println("Writer is null or empty);   
    erros.rejectValue("writer", "trouble");   
  }   
...   
}
