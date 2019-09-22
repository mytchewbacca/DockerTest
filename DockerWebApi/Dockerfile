# get base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy the CSPROJ file and restore any dependencies (via NUGET0)
COPY *.csproj ./
RUN dotnet restore

#Copy the project files and build our release
COPY . ./
RUN dotnet publish -c Release -o /out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build-env /out .
ENTRYPOINT ["dotnet", "DockerWebApi.dll"]