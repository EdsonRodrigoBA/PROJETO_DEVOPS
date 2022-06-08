#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:80
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["./src/InicioDevops.Curso.Service/InicioDevops.Curso.Service.csproj", "src/InicioDevops.Curso.Service/"]
RUN dotnet restore "src/InicioDevops.Curso.Service/InicioDevops.Curso.Service.csproj"
COPY . .
WORKDIR "/src/src/InicioDevops.Curso.Service"
RUN dotnet build "InicioDevops.Curso.Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "InicioDevops.Curso.Service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "InicioDevops.Curso.Service.dll"]