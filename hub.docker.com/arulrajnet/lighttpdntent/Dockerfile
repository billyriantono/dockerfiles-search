FROM steinhoem/rl2019api
RUN mkdir /app/logs
RUN chmod g+w /app/logs
RUN chown -R :dockerrunner /app
EXPOSE 8000
ENTRYPOINT ["dotnet", "Prod.Api.dll", "--urls=http://rl2019api.artsdatabanken.no:8000"]