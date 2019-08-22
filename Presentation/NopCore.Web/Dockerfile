FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Presentation/NopCore.Web/NopCore.Web.csproj", "Presentation/NopCore.Web/"]
RUN dotnet restore "Presentation/NopCore.Web/NopCore.Web.csproj"
COPY . .
WORKDIR "/src/Presentation/NopCore.Web"
RUN dotnet build "NopCore.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NopCore.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NopCore.Web.dll"]