FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /ClassifiedAds.Microservices

# Copy csproj and restore as distinct layers
COPY ./Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot/*.csproj ./Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot/
RUN dotnet restore ./Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot.csproj

# Copy everything else and build
COPY . ./
RUN dotnet publish ./Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot/ClassifiedAds.Gateways.Ocelot.csproj -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /ClassifiedAds.Microservices
COPY --from=build-env /ClassifiedAds.Microservices/out .

ENTRYPOINT ["dotnet", "ClassifiedAds.Gateways.Ocelot.dll"]