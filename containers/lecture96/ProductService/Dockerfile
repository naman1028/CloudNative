FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build      # serves as the base image, set alias as build for reference in later stag
WORKDIR /src    # set working directory inside the container
COPY ProductService.csproj . # copy only the project file(.csproj) leveraging Docker cache for faster builds in woring directory
RUN dotnet restore # restore dependencies listed in the project file
COPY . .  # copy all files in the current directory to the working directory in the container
RUN dotnet publish -c release -o /app # publis/compile applicon in release configuration to the /app folder

FROM mcr.microsoft.com/dotnet/aspnet:7.0 # final  # use the ASP.NET runtime image for the final image
WORKDIR /app # set working directory inside the container
COPY --from=build /app .# copy the published application from the build stage to the working directory
ENTRYPOINT ["dotnet", "ProductService.dll"] # set the command to run the application