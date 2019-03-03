FROM microsoft/dotnet-framework:4.6.1-sdk AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY TestWebapp/*.csproj ./TestWebapp/
RUN nuget restore

# copy everything else and build app
COPY TestWebapp/. ./TestWebapp/
WORKDIR /app/TestWebapp
RUN msbuild /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.6.1 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/TestWebapp/. ./
