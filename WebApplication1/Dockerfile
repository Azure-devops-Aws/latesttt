# Set the base image to use for the container
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project files to the working directory
COPY . .

# Restore the NuGet packages
#RUN dotnet restore

# Build the application
RUN dotnet build --configuration Release --no-restore

# Publish the application
RUN dotnet publish --configuration Release --no-restore --output /app/publish

# Set the base image to use for the runtime container
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime

# Set the working directory inside the runtime container
WORKDIR /app

# Copy the published files from the build container to the runtime container
COPY --from=build /app/publish .

# Expose the desired port(s) that the application will listen on
EXPOSE 80

# Set the entry point for the container
ENTRYPOINT ["dotnet", "YourMvcApp.dll"]
