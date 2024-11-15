FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5178

ENV ASPNETCORE_URLS=http://+:5178

USER app
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG configuration=Release
WORKDIR /src
COPY ["ConferenceAttendees.Api/ConferenceAttendees.Api.csproj", "ConferenceAttendees.Api/"]
RUN dotnet restore "ConferenceAttendees.Api/ConferenceAttendees.Api.csproj"
COPY . .
WORKDIR "/src/ConferenceAttendees.Api"
RUN dotnet build "ConferenceAttendees.Api.csproj" -c $configuration -o /app/build

FROM build AS publish
ARG configuration=Release
RUN dotnet publish "ConferenceAttendees.Api.csproj" -c $configuration -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConferenceAttendees.Api.dll"]
