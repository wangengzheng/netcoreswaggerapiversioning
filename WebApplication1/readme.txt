apiversion
	url:https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx
	nuget: netcore https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.

	cmd: Install-Package Microsoft.AspNetCore.Mvc.Versioning -Version 2.3.0
	use: services.AddMvc();
		 services.AddApiVersioning();

    controller:
		[ApiVersion("1",Deprecated =true)]
		[ApiVersion("2")]
		[Route("api/v{version:apiVersion}/[controller]")]
		[ApiController]
		public class ValuesController : ControllerBase

	method:
		// DELETE api/values/5
        [MapToApiVersion("2")]
        [HttpDelete("{id}")]
        public void Delete(int id)
        {
        }


swagger
	nuget : netcore install Install-Package Swashbuckle.AspNetCore
	url:https://www.nuget.org/packages/Swashbuckle.AspNetCore/5.0.0-beta
	cmd : Install-Package Swashbuckle.AspNetCore -Version 5.0.0-beta
	use:
		 services.AddSwaggerGen(c =>
			{
				c.SwaggerDoc("v1", new Info { Title = "My API", Version = "v1" });
			});

		 app.UseSwagger();

		// Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.), 
		// specifying the Swagger JSON endpoint.
		app.UseSwaggerUI(c =>
		{
			c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
		});


