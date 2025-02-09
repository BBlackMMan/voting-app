
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /app

COPY . .

RUN rm -rf obj/ project.assets.json

RUN dotnet add package Newtonsoft.Json --version 13.0.1

RUN dotnet nuget locals all --clear && dotnet restore

RUN dotnet list package

RUN ls -l /app

RUN dotnet build -c Release --no-restore

RUN dotnet publish -c Release --self-contained false --no-restore -o /publish

FROM mcr.microsoft.com/dotnet/runtime:7.0

WORKDIR /app

COPY --from=build /publish .

CMD ["dotnet", "Worker.dll"]
