FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["testJenkins/testJenkins.csproj", "testJenkins/"]
RUN dotnet restore "testJenkins/testJenkins.csproj"
COPY . .
WORKDIR "/src/testJenkins"
RUN dotnet build "testJenkins.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "testJenkins.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testJenkins.dll"]