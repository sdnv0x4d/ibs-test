FROM mcr.microsoft.com/dotnet/sdk:6.0 AS builder

WORKDIR /build
COPY *.csproj .

RUN dotnet restore

COPY ./* .
RUN dotnet publish -c release -o /app --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /opt/app
COPY --from=builder /app .

RUN useradd --shell /bin/false appuser && \
    chown -R appuser:appuser /opt/app

USER appuser

EXPOSE 80

ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]
