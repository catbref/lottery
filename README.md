# Lottery

## How to build

`mvn clean`
`mvn package`
`mvn install dependency:copy-dependencies`

## How to use

For usage:\
    `java -cp 'target/qortal-lottery-1.0.0.jar:target/dependency/*' org.qortal.at.lottery.Lottery`

Example use:\
    `java -cp 'target/qortal-lottery-1.0.0.jar:target/dependency/*' org.qortal.at.lottery.Lottery 20160 0.1`

Produces AT creation bytes:\
    `1i7sLQfQb3JU6Wek6x1bezdWAPyBso43vchvJMokNcp7M11wrqQZjHoh9xL4hkDPb2GgkiUxqvotuhBpdLptoiSnc8FsjFgv8mjshtSoHx6HjJa3GfA6dJAud4nYyarxq7EhzLYWqFYqf539Sjb3vCJvdGaHETrTQBwHRfWcgF79kHCmdmsBkUknZ5otKj25QccwUS7Pi6w1oRNS8YiX4ntecopmLwWunjTvXphXa6YCiW6pDo45iBZHH48byvKjcPkS7QzsT77S6cULGAyVHwcXRQLhbZRz2qwD1BG42FENzLDw5zDaLDpLzuN5E9PimqC2ZLE687JLPDa7AixVsrwAKQNEx6nWRCW5y8CoFJqbDASk2T3U9dg7QiAPLAJ25oDMVs3ZeMRGTDkTZapocg4SZBbJRvP1JHg5sYNQ8X1osKjakvVBf6zMaip6E3NFZWAw3G415H5Cb6TKXrh1W7Lc2HQ8D9NjZDE86dgoCSrFNNkhcJR3RGvdLxK3TnM5isBX2nY7zbLRSNkmS4YQRpRJeTyBPTBFFQUQnpoS8wpxfHZhhPSYF59mPZwDn8cCvJCNzjfGy91ZNqKwpP8mceoVieh4GVkFF99YoR5y8wRXMdvvxQVnU1GUeg1PKYzt9HRmGTigWaT8DuTDxzpDm38s89X5U4jGMigGeh5u9m14RcZ5ZF9ReZq2Cg4vtf6L3D1i6pNERZK2oFZZ2unxxDi49hLsatV2i4UhcQv1pzkU5tny7vViX6arDmYB95DLjG5jBQoP31nCbJVtKo3cygLVGrgQrY5ZACnqntmFSzBcbbpdm2Z85g2h8Uh4rtBVNqr4SWBvbaxMpnMsPD1pJAg5nkXgJ7y6EM32rcy4mcLwPkU9fdqLrmaMr84jc9bCF2jEcJbc6oTD483yyv6ekkwuGoapn3FVdXjUZD`

Creation bytes can be passed to `qort-tx` script as part of a `DEPLOY-AT` transaction:\
    `qort-tx DEPLOY_AT <privkey> <name> <description> <aTType> <tags> <creationBytes> <amount>`

So using example above, front-loading lottery with 100.0 QORT (which also covers AT fees):\
    `description="lottery test: payout in 2 weeks, send minimum 0.1 QORT to enter"`\
    `creation_bytes=$(java -cp 'target/qortal-lottery-1.0.0.jar:target/dependency/*' org.qortal.at.lottery.Lottery 20160 0.1 | tail +2)`\
    `qort-tx -s -p DEPLOY_AT private-key-in-base58 'lottery-test' "$description" 'lottery' 'lottery' $creation_bytes 100.0`
