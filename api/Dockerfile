# Build Stage
FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /api

COPY api.csproj .

# ISD firewallers should uncommnent the lines below
#ENV 	http_proxy=http://10.88.20.11:8080 \
#	https_proxy=http://10.88.20.11:8080 \
#	no_proxy="You know what to put here!"

RUN dotnet restore

COPY . .
RUN dotnet publish -o /publish

# Runtime Image Stage
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /publish
COPY --from=build-env /publish .
ENTRYPOINT ["dotnet", "api.dll"]