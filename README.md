# Python-code-to-make-discord-moderation-bot

import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='/')

@bot.event
async def on_ready():
    print(f'{bot.user} has connected to Discord!')

@bot.command(name='hello')
async def hello(ctx):
    await ctx.send(f'Hello, {ctx.author.mention}!')

@bot.command(name='roll')
async def roll(ctx, sides: int):
    await ctx.send(f'You rolled a {random.randint(1, sides)}!')

@bot.command(name='kick')
@commands.has_permissions(kick_members=true)
async def kick(ctx, member: discord.Member, reason=None):
    await member.kick(reason=reason)
    await ctx.send(f'{member.mention} has been kicked!')

@bot.command(name='ban')
@commands.has_permissions(ban_members=true)
async def ban(ctx, member: discord.Member, reason=None):
    await member.ban(reason=reason)
    await ctx.send(f'{member.mention} has been banned!')

@bot.command(name='mute')
@commands.has_permissions(manage_roles=true)
async def mute(ctx, member: discord.Member, time: int):
    role = discord.utils.get(ctx.guild.roles, name='Muted')
    await member.add_roles(role)
    await ctx.send(f'{member.mention} has been muted for {time} minutes!')

@bot.command(name='unmute')
@commands.has_permissions(manage_roles=true)
async def unmute(ctx, member: discord.Member):
    role = discord.utils.get(ctx.guild.roles, name='Muted')
    await member.remove_roles(role)
    await ctx.send(f'{member.mention} has been unmuted!')

bot.run('YOUR_DISCORD_BOT_TOKEN')
