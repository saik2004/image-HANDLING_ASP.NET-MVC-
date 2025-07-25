# image-HANDLING_ASP.NET-MVC-

```
public IActionResult Create(Brand brand)
{

    string webRootPath = _WebHostEnvironment.WebRootPath;

    var file = HttpContext.Request.Form.Files;


    if(file.Count>0 )
    {
        string newFileName = Guid.NewGuid().ToString();

        var upload = Path.Combine(webRootPath, @"images\brand");

        var extension = Path.GetExtension(file[0].FileName);

        using (var filestream = new FileStream(Path.Combine(upload, newFileName + extension), FileMode.Create))
        {
            file[0].CopyTo(filestream);
        }

        brand.BrandLogo = @"\images\brand\" + newFileName + extension; 
    }
    if (ModelState.IsValid)
    {
        _dbcontext.Brand.Add(brand);
        _dbcontext.SaveChanges();

        return RedirectToAction(nameof(Index)); 
    }
    return View();
}
```
