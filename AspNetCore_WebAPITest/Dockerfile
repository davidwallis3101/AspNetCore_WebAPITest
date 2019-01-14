FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AspNetCore_WebAPITest/AspNetCore_WebAPITest.csproj", "AspNetCore_WebAPITest/"]
RUN dotnet restore "AspNetCore_WebAPITest/AspNetCore_WebAPITest.csproj"
COPY . .
WORKDIR "/src/AspNetCore_WebAPITest"
RUN dotnet build "AspNetCore_WebAPITest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetCore_WebAPITest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCore_WebAPITest.dll"]